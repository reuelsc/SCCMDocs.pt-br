---
title: Versões de visualização técnica
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 07/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cb49531bd6d10106b17cca65218d7158c24dc3e
ms.sourcegitcommit: 5a36200c738f20a78299a30723c8e613af71efce
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843857"
---
# <a name="technical-preview-for-configuration-manager"></a>Visualização técnica para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo fornece detalhes sobre o branch de visualização técnica mensal do Configuration Manager. A visualização técnica introduz uma nova funcionalidade na qual a Microsoft tem trabalhado. Ele introduz novos recursos que ainda não estão incluídos no branch atual do Configuration Manager. Eventualmente, esses recursos poderão ser incluídos em uma atualização do branch atual. Antes de finalizarmos os recursos, queremos que você os experimente e dê sua opinião.  

Como esta versão é technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do branch da visualização técnica do Configuration Manager. Este artigo lista cada novo recurso juntamente com a versão da visualização técnica na qual ele aparece pela primeira vez. Por exemplo, a versão **1901** de janeiro (01) de 2019 (19). Os artigos separados dedicados a cada detalhe da versão prévia detalham recursos individuais.  

Para saber mais sobre o que há de novo no *branch atual* do Configuration Manager, confira [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole a seguinte URL em seu leitor de feeds de RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requisitos e limitações  

> [!IMPORTANT]  
> A visualização técnica é licenciada apenas para ser usada em um ambiente de laboratório. A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software em visualizações técnicas. Além disso, o software de visualização técnica pode ter padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

Para a maioria dos pré-requisitos do produto, use as informações contidas nas [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations). As seguintes exceções se aplicam ao branch da visualização técnica:  

- Cada instalação fica ativa por 90 dias antes de se tornar inativa.  

- O inglês é o único idioma com suporte.  

- Só há suporte para os seguintes parâmetros de linha de comando de configuração:  

    - `/silent`  
    - `/testdbupgrade`  

- O ponto de conexão de serviço deve ser instalado no modo online. Ele não é compatível com o modo offline.  

- Os artigos separados para cada versão específica do technical preview incluem requisitos ou limitações adicionais, conforme aplicável.

- Os recursos a seguir não são compatíveis com o branch da visualização técnica:  

    - [Migração](/sccm/core/migration/migrate-data-between-hierarchies) de ou para esse o branch de visualização.  

    - [Faça upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) para esse o branch de visualização.  

    - [Recuperação de site](/sccm/core/servers/manage/recover-sites) na pasta cd.latest.  <!--507106-->

- Não há suporte para atualização para o branch atual a partir deste o branch de visualização.  

    > [!Note]  
    > Quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de upgrade no console, confira [Instalação dos pacotes de atualização do Configuration Manager](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  

- Ele só é compatível com um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

O branch de visualização técnica do Configuration Manager é compatível com os seguintes produtos e tecnologias:

- Só há suporte para as seguintes versões do **SQL Server**:  

    - SQL Server 2017 (com atualização cumulativa 2 ou posterior)
    - SQL Server 2016 (sem service pack ou posterior)
    - SQL Server 2014 (com o service pack 1 ou posterior)
    - SQL Server 2012 (com o service pack 3 ou posterior)  

- O site dá suporte a até 10 clientes, que devem executar uma das seguintes versões do Windows:  

    - Windows 10  
    - Windows 8.1  
    - Windows 7  

> [!Note]  
> A inclusão desses produtos nesse conteúdo não implica uma extensão de suporte para uma versão além do seu ciclo de vida de suporte. O Configuration Manager não oferece suporte a produtos além do ciclo de vida de suporte. Para mais informações, confira [Política de Ciclo de Vida da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

## <a name="bkmk_install"></a> Instalar e atualizar  

O branch de visualização técnica do Configuration Manager para uso em laboratórios é diferente do branch atual do Configuration Manager para uso em produção.  

Primeiro, é necessário instalar uma versão de linha de base do branch da visualização técnica. Depois de instalar uma versão de linha de base, use as atualizações no console para atualizar sua instalação para a versão prévia mais recente. Normalmente, as novas versões da visualização técnica são disponibilizadas todos os meses.

A Microsoft oferece suporte a todas as versões da visualização técnica até que três versões sucessivas estejam disponíveis. Por exemplo, quando a versão 1708 foi liberada, a versão 1704 deixou de ter suporte. As versões 1705, 1706 e 1707 permaneceram com suporte. Quando uma linha de base fica sem suporte, ainda há suporte para a instalação um novo site da visualização técnica desde que você atualize imediatamente para uma versão com suporte. A linha de base mais antiga terá suporte até que uma nova versão de linha de base esteja disponível. Atualize para a versão mais recente disponível na linha de base e repita o processo de atualização até instalar a versão mais recente da visualização técnica.

> [!TIP]  
> Quando você instala uma atualização do Technical Preview, atualiza a instalação da versão prévia para essa nova versão de Technical Preview. Uma instalação da visualização técnica nunca tem a opção de upgrade para uma instalação de branch atual. Ela também não recebe atualizações da versão de branch atual.
>
> Diversas vezes ao longo do ano, são disponibilizadas versões do branch da visualização técnica e do branch atual com o mesmo número de versão. Por exemplo, há um visualização técnica versão 1802 e um branch atual versão 1802.

### <a name="active-baseline-versions"></a>Versões de linha de base ativas

Instale uma versão de linha de base em até um ano após seu lançamento. Quando você instala um novo site da visualização técnica, se mais de uma versão de linha de base estiver disponível no momento, use a versão de linha de base mais recente.

- **Visualização Técnica versão 1907**: A visualização técnica do Configuration Manager versão 1907 está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base do [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


## <a name="BKMK_TPFeedback"></a> Enviando comentários  

Adoramos ouvir seus comentários sobre os novos recursos da visualização técnica. Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página do UserVoice](https://configurationmanager.uservoice.com).  


<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->


## <a name="bkmk_tpCaps"></a> Recursos da versão mais recente  

Os seguintes recursos estão disponíveis com a visualização técnica mais recente do Configuration Manager versão:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1907"></a>Visualização Técnica versão 1907

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Pesquisar no editor de sequência de tarefas](/sccm/core/get-started/2019/technical-preview-1907#bkmk_tsedit) <!--4621085-->
- [Aprimoramentos no painel de preparação de atualização do Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1907#improvements-to-office-365-proplus-upgrade-readiness-dashboard) <!--4021125-->

> [!Note]  
> Os recursos que estavam disponíveis em uma versão anterior da visualização técnica permanecem disponíveis em versões posteriores. De forma semelhante, os recursos que foram adicionadas ao branch atual do Configuration Manager permanecem disponíveis no branch da visualização técnica.  


## <a name="features-in-recent-technical-previews"></a>Recursos em visualizações técnicas recentes

Os recursos a seguir foram lançados com versões anteriores do branch de visualização técnica do Configuration Manager desde o último lançamento do branch atual:

> [!Tip]  
> Quando uma nova versão do branch atual estiver disponível, os recursos que estão disponíveis nessa versão estarão listados no artigo *Novidades* mais recente. Para obter mais informações, consulte [Novidades em versões incrementais](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

<!-- This is the full list of new features in the past TP releases since the last CB release. 
Each month, add features from the list above to a new H3 section at the top of this section. 
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

### <a name="technical-preview-version-1906"></a>Visualização Técnica versão 1906

- [Melhorias nas tarefas de manutenção](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-maintenance-tasks) <!--3555894-->
- [Monitoramento de atualização do banco de dados de atualização do Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#configuration-manager-update-database-upgrade-monitoring) <!--4200581-->
- [Vários grupos piloto para cargas de trabalho de cogerenciamento](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt_pilot) <!--3555750-->
- [Lógica de notificação reprojetada para software recentemente disponível](/sccm/core/get-started/2019/technical-preview-1906#redesigned-notification-logic-for-newly-available-software) <!--3555904-->
- [RBAC em pastas](/sccm/core/get-started/2019/technical-preview-1906#rbac-on-folders) <!--3600867-->
- [Descoberta de grupo de usuários do Azure Active Directory](/sccm/core/get-started/2019/technical-preview-1906#bkmk_aad-disco) <!--3611956-->
- [Controle remoto em qualquer lugar usando o gateway de gerenciamento de nuvem](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) <!--4575930-->
- [Melhorias no Hub de Comunidade](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) <!--3555935-->
- [Adicionar junções, operadores adicionais e agregadores no CMPivot](/sccm/core/get-started/2019/technical-preview-1906#bkmk_cmpivot) <!--4054074-->
- [Melhorias ao CMPivot](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-cmpivot) <!--4619340,4683130-->
- [Melhorias no console do Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#bkmk_console) <!--4223683-->
- [Suporte para a Área de Trabalho Virtual do Windows](/sccm/core/get-started/2019/technical-preview-1906#bkmk_winsku) <!--3556025-->
- [Notificações de contagem regressiva mais frequentes para reinicializações](/sccm/core/get-started/2019/technical-preview-1906#more-frequent-countdown-notifications-for-restarts) <!--3976435-->
- [Registro automático do cogerenciamento usando o token de dispositivo](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt) <!--4454491-->
- [Opções adicionais para catálogos de atualizações de terceiros](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) <!--4469002-->
- [Limpar conteúdo do aplicativo do cache do cliente durante a sequência de tarefas](/sccm/core/get-started/2019/technical-preview-1906#bkmk_tscache) <!--4485675-->
- [Novo Windows 10, versão 1903 e categoria de produto mais recente](/sccm/core/get-started/2019/technical-preview-1906#new-windows-10-version-1903-and-later-product-category) <!--4682946-->
- [Regra de insights de gerenciamento para fallback de NTLM](/sccm/core/get-started/2019/technical-preview-1906#bkmk_ntlm) <!--4572953-->
- [Filtrar os aplicativos implantados em dispositivos](/sccm/core/get-started/2019/technical-preview-1906#bkmk_appcategory) <!--4451056-->
- [Melhorias na implantação do sistema operacional](/sccm/core/get-started/2019/technical-preview-1906#bkmk_osd) <!--4668846, 2840337, 4512937-->
- [Link direto para guias personalizadas no Centro de Software](/sccm/core/get-started/2019/technical-preview-1906#bkmk_swctr) <!--4655176-->

### <a name="technical-preview-version-1905"></a>Visualização Técnica versão 1905

- [Controle aprimorado sobre a manutenção do WSUS](/sccm/core/get-started/2019/technical-preview-1905#improved-control-over-wsus-maintenance) <!--4110109-->
- [Melhorias no console do Configuration Manager](/sccm/core/get-started/2019/technical-preview-1905#bkmk_console) <!--4616810-->
- [Configurar o tempo de execução máximo padrão para atualizações de software](/sccm/core/get-started/2019/technical-preview-1905#bkmk_timeout) <!--3734426-->
- [Critérios de confiança do arquivo sobre o Windows Defender Application Guard](/sccm/core/get-started/2019/technical-preview-1905#bkmk_wdag) <!--3555858-->
- [Grupos de aplicativos](/sccm/core/get-started/2019/technical-preview-1905#bkmk_app-group) <!--3555907-->
- [Sequência de tarefas como um tipo de implantação do modelo de aplicativo](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) <!--3555953-->
- [Gerenciamento do BitLocker](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) <!--3601034-->
- [Depurador da sequência de tarefas](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdebug) <!--3612274-->
- [Painel de fontes de dados do cliente da Otimização de Entrega](/sccm/core/get-started/2019/technical-preview-1905#bkmk_do) <!--3555759-->
- [Melhorias no Hub de Comunidade](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) <!--4224401-->
- [Exibir GUID SMBIOS nas listas de dispositivos](/sccm/core/get-started/2019/technical-preview-1905#bkmk_smbios) <!--4526580-->
- [Visualizador de log OneTrace](/sccm/core/get-started/2019/technical-preview-1905#bkmk_onetrace) <!--3555962-->
- [Melhorias na infraestrutura do Centro de Software ](/sccm/core/get-started/2019/technical-preview-1905#bkmk_swctr) <!--3555950-->
- [Melhorias nas personalizações da guia do Centro de Software](/sccm/core/get-started/2019/technical-preview-1905#improvements-to-software-center-tab-customizations) <!--4063773-->
- [Melhorias nas aprovações de aplicativos](/sccm/core/get-started/2019/technical-preview-1905#bkmk_approve) <!--4224910-->
- [Tentar novamente e instalar aplicativos previamente aprovadas](/sccm/core/get-started/2019/technical-preview-1905#bkmk_retry) <!--4336307-->
- [Instalar aplicativos em um dispositivo](/sccm/core/get-started/2019/technical-preview-1905#bkmk_device-app) <!--4402180-->
- [Notificações de contagem regressiva mais frequentes para reinicializações](/sccm/core/get-started/2019/technical-preview-1905#bkmk_restart) <!--3976435-->
- [Sincronizar os resultados de associação de coleção para grupos do Active Directory do Azure](/sccm/core/get-started/2019/technical-preview-1905#bkmk_aadcollsync) <!--3607475-->
- [Configurar o período de retenção mínimo de cache do cliente](/sccm/core/get-started/2019/technical-preview-1905#bkmk_cache) <!--4485509-->
- [Melhorias na implantação do sistema operacional](/sccm/core/get-started/2019/technical-preview-1905#bkmk_osd) <!--4512937,4224642-->
- [Adicionar um nó SQL AlwaysOn](/sccm/core/get-started/2019/technical-preview-1905#bkmk_sqlao) <!--3127336-->

### <a name="technical-preview-version-1904"></a>Visualização Técnica versão 1904

- [Painel de preparação de atualização do Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) <!--4021125-->  
- [Configurar a atualização dinâmica durante as atualizações de recursos](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) <!--4062619-->  
- [GitHub e o Hub de Comunidade](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) <!--3555935,3555936-->  
- [CMPivot autônomo](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) <!--3555890-->  
- [Melhorias na infraestrutura do Centro de Software ](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) <!--3555950-->  
- [Controle aprimorado sobre a manutenção do WSUS](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) <!--4110109-->  
- [Pacotes de driver de pré-cache e imagens do sistema operacional](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) <!--4224642-->  
- [Melhorias na implantação do sistema operacional](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) <!--2839943,4447680-->  

### <a name="technical-preview-version-1903"></a>Technical Preview versão 1903

- [Estimador de custo de serviços de nuvem](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) <!--3555774-->  
- [Use seu ponto de distribuição como um servidor de cache local para a Otimização de Entrega](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) <!--3555764-->  
- [Recuperar o bloqueio para editar sequências de tarefas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) <!--3699337-->  
- [Detalhar atualizações necessárias](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) <!--4224414-->  
- [Melhoria na criação de mídia de sequência de tarefas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) <!--4090666-->  


## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Recurso        | Versão da visualização técnica |  
|----------------|---------------------------|
| Baixar relatórios do Hub de Comunidade<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Hub de Comunidade <!--3556020, fka 1357766--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Serviço de respondente PXE baseado no cliente <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Suporte de inicialização de rede PXE para IPv6 <!--3601254, fka 1269793--> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Usar o Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Melhorias do Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Os usuários finais podem instalar aplicativos do Portal da Empresa <!--3601249, fka 1037233--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |


## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os seguintes artigos:  

- [Avaliar o Configuration Manager em um laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
>
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
