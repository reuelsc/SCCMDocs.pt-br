---
title: Versões de visualização técnica
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2909de734954d9519c04bc02012c3bfe17c9b81f
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802505"
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
> A visualização técnica é licenciada apenas para ser usada em um ambiente de laboratório. A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão prévia. Além disso, o software de versão prévia pode ter padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

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

- **Technical Preview versão 1902.2**: O Configuration Manager Technical Preview versão 1902.2 está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base do [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Enviando comentários  

Adoramos ouvir seus comentários sobre os novos recursos da visualização técnica. Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página do UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> Recursos da versão mais recente  

Os seguintes recursos estão disponíveis com a visualização técnica mais recente do Configuration Manager versão:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1903"></a>Technical Preview versão 1903

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Estimador de custo de serviços de nuvem](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) <!--3555774-->  

- [Use seu ponto de distribuição como um servidor de cache local para a Otimização de Entrega](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) <!--3555764-->  

- [Recuperar o bloqueio para editar sequências de tarefas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) <!--3699337-->  

- [Detalhar atualizações necessárias](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) <!--4224414-->  

- [Melhoria na criação de mídia de sequência de tarefas](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) <!--4090666-->  

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
 | Idiomas adicionais para atualizações do Office 365 <!--3555955--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365lang) | Versão 1902 |
 | Integração com análises para a preparação do Office 365 ProPlus <!--3735402--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365) | Versão 1902 |
 | Melhoria dos critérios de sucesso da implantação em fases <!--3555946--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_pod) | Versão 1902 |
 | Melhoria no HTTP aprimorado <!--3798957--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_ehttp) | Versão 1902 |
 | Substituir as notificações do sistema por uma janela de diálogo <!--3555947--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact) | Versão 1902 |
 | Status do andamento durante a sequência de tarefas de atualização in-loco <!--3747129--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu) | Versão 1902 |
 | Redirecionar as pastas conhecidas do Windows para o OneDrive <!--3556021--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb) | Versão 1902 |
 | Exibir a primeira tela somente durante o controle remoto <!--3231732--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti) | Versão 1902 |
 | Editar ou copiar scripts do PowerShell <!--3705507--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit) | Versão 1902 |
 | Adicionar o Gateway de Gerenciamento de Nuvem a grupos de limites <!--3640932--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg) | Versão 1902 |
 | Configurar as exibições padrão no Centro de Software <!--3612112--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr) | Versão 1902 |
 | Melhoria no painel de integridade do cliente <!--3599209--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health) | Versão 1902 |
 | Painel de integridade do cliente <!--3599209--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | Versão 1902 |
 | Especificar a prioridade das atualizações de recurso nos serviços do Windows 10 <!--3734525--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | Versão 1902 |
 | Monitoramento dedicado para implantações em fases <!--3555949--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | Versão 1902 |
 | Executar o CMPivot no site de administração central <!--3610960--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | Versão 1902 |
 | Melhorias na etapa da sequência de tarefas Executar Script do PowerShell <!--3556028--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | Versão 1902 |
 | Produtos do Office no painel de ciclo de vida <!--3556026--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | Versão 1902 |
 | Regras de insight de gerenciamento para coleções <!--3555752--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | Versão 1902 |
 | Pesquisar exibições de dispositivo usando o endereço MAC <!--3600878--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | Versão 1902 |
 | Modo de manutenção do ponto de distribuição <!--3555754--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | Versão 1902 |
 | Serviço de imagens otimizado <!--3555951--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | Versão 1902 |
 | Importar um índice único de uma imagem do sistema operacional <!--3719699--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | Versão 1902 |
 | Usar o Azure Resource Manager para os serviços de nuvem <!--3605704--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | Versão 1902 |
 | Confirmação de comentários do console <!--3556010--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | Versão 1902 |
 | Criar um laboratório do Configuration Manager Technical Preview no Azure <!--3556017--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | Não aplicável |
 | Especificar uma porta personalizada para ativação de par <!--3605925--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | Versão 1902 |
 | Exibir consoles conectados recentemente <!--3699367--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | Versão 1902 |
 | Interromper o serviço de nuvem quando ele exceder o limite <!--3735092--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | Versão 1902 |
 | Tempo limite do modo de provisionamento do cliente <!--3197824--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | Versão 1902 |
 | Melhorias na implantação do sistema operacional <!--3633146,3641475,3654172,3734270--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | Versão 1902 |
 | Melhorias na etapa da sequência de tarefas Executar Script do PowerShell <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | Versão 1902 |
 | Melhorias nas aprovações de aplicativo por email <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | Versão 1902 |
 | Configurar a afinidade de dispositivo do usuário no Centro de Software <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | Versão 1902 |
 | Melhorias no console do Configuration Manager <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | Versão 1902 |
 | Baixar relatórios do Hub de Comunidade<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Não foi adicionado](media/Red_X.gif) |

## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Recurso        | Versão da visualização técnica |  
|----------------|---------------------------|
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
