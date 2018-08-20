---
title: Informações de gerenciamento
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de insights de gerenciamento disponível no console do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 92f82ee7247030d19df63e50b0ac4437f250717a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383490"
---
# <a name="management-insights-in-configuration-manager"></a>Insights de gerenciamento no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os insights de gerenciamento do Configuration Manager fornecem informações sobre o estado atual do ambiente. As informações baseiam-se na análise de dados do banco de dados do site. As informações ajudam você a melhor compreender seu ambiente e executar ações com base nas informações. Esse recurso foi lançado no Configuration Manager versão 1802. <!--1353967-->



## <a name="review-management-insights"></a>Examinar insights de gerenciamento 

Para exibir as regras, sua conta precisa da permissão de **leitura** no objeto **site**.

1. Abra o Console do Configuration Manager.  

2. Acesse o espaço de trabalho **Administração** e clique em **Insights de Gerenciamento**.  

3. Selecione **Todos os Insights**.  

4. Clique duas vezes no **Nome do Grupo de Insight de Gerenciamento** que deseja examinar. Ou realce-o e clique em **Mostrar Insights** na faixa de opções.  

As quatro guias a seguir estão disponíveis para revisão: 

- **Todas as Regras**: fornece a lista completa de regras do grupo de insight de gerenciamento escolhido.  

- **Completo**: lista as regras em que nenhuma ação é necessária.  

- **Em Andamento**: mostra as regras em que alguns, mas nem todos os pré-requisitos foram atendidos.  

- **Ação Necessária**: as regras que precisam de ações executadas são listadas. Clique com o botão direito do mouse e selecione **Mais Detalhes** para recuperar itens específicos nos quais uma ação é necessária.  

O painel **Pré-requisitos** lista os itens necessários para executar a regra.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas as regras e os pré-requisitos do grupo de serviços de nuvem
![Insights de gerenciamento – Todas as regras e os pré-requisitos do grupo de serviços de nuvem](./media/Management-insights-all-cloud-rules.png)


Selecione uma regra e clique em **Mais Detalhes** para ver os detalhes da regra.



## <a name="operations"></a>Operações

As regras dos insights de gerenciamento reavaliam sua aplicabilidade de acordo com um agendamento semanal. Para reavaliar uma regra sob demanda, clique com o botão direito do mouse na regra e selecione **Reavaliar**.

O arquivo de log das regras de insight de gerenciamento está em **SMS_DataEngine.log** no servidor do site.

<!--1357930--> Começando na versão 1806, algumas regras permitem executar uma ação. Selecione uma regra, clique em **Mais Detalhes** e, se disponível, clique em **Executar ação**. 

Dependendo da regra, essa ação tem um dos seguintes comportamentos:  

- Navegar automaticamente no console até o nó, onde você pode realizar outras ações. Por exemplo, se a percepção do gerenciamento recomenda alterar uma configuração de cliente, a ação leva para o nó Configurações do Cliente. Em seguida, execute outras ações modificando o objeto de configurações do cliente padrão ou personalizadas.  

- Navegar para uma visualização filtrada com base em uma consulta. Por exemplo, a ação na regra de coleções vazias mostra apenas essas coleções na lista de coleções. Em seguida, execute outras ações, como excluir uma coleção ou modificar suas regras de associação.  



## <a name="groups-and-rules"></a>Grupos e regras

As regras são organizadas em diferentes grupos de insights de gerenciamento. Consulte a lista a seguir para saber quais grupos e regras estão disponíveis no momento:


### <a name="applications"></a>Aplicativos

Insights do gerenciamento de aplicativos.

- **Aplicativos sem implantações**: lista os aplicativos em seu ambiente que não têm implantações ativas. Essa regra ajuda você a encontrar e excluir aplicativos não utilizados para simplificar a lista de aplicativos exibidos no console. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).  


### <a name="cloud-services"></a>Cloud Services

Ajuda você a integrar vários serviços de nuvem, o que permite o gerenciamento moderno de seus dispositivos. 

- **Avaliar a preparação para o cogerenciamento**: ajuda você a entender quais etapas são necessárias para habilitar o cogerenciamento. Essa regra tem pré-requisitos. Para obter mais informações, confira [Visão geral do cogerenciamento](/sccm/core/clients/manage/co-management-overview).  

- **Configurar serviços do Azure para serem usados com o Configuration Manager**: essa regra ajuda você a integrar o Configuration Manager ao Azure AD, o que permite que os clientes se autentiquem no site usando o Azure AD. Para obter mais informações, consulte [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Habilitar dispositivos para ingressarem no Azure Active Directory híbrido**: os dispositivos que ingressaram no Azure AD permitem que os usuários entrem com suas credenciais de domínio, o que garante que os dispositivos atendam aos padrões de segurança e conformidade da organização. Para obter mais informações, confira [Considerações de design de identidade do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Atualizar clientes para a versão mais recente do Windows 10**: o Windows 10, versão 1709 ou acima melhora e moderniza a experiência de computação dos usuários. Para obter mais informações, confira [Principais artigos sobre a adoção do Windows como serviço](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Coleções

Insights que ajudam a simplificam o gerenciamento limpando e reconfigurando coleções.

- **Coleções vazias**: lista as coleções no seu ambiente que não têm membros. Para obter mais informações, confira [Como gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections).  


### <a name="proactive-maintenance"></a>Manutenção proativa
<!--1352184--> Começando na versão 1806, as regras deste grupo destacam possíveis problemas de configuração que podem ser evitados por meio da manutenção dos objetos do Configuration Manager.    

- **Grupos de limites sem sistemas de sites atribuído**: sem sistemas de sites atribuídos, os grupos de limites só podem ser usados para atribuição de site. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Grupos de limites sem membros**: grupos de limites não serão aplicáveis para a pesquisa de conteúdo ou a atribuição de site se não tiverem membros. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Pontos de distribuição que não fornecem conteúdo aos clientes**: pontos de distribuição que ainda não forneceram conteúdo aos clientes nos últimos 30 dias. Esses dados se baseiam nos relatórios de clientes de seu histórico de download. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Habilitar limpeza do WSUS**: verifica se você habilitou a opção de executar a limpeza do WSUS nas propriedades do componente de ponto de atualização de software. Essa opção ajuda a melhorar o desempenho do WSUS. Para obter mais informações, confira [Manutenção de atualização de software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Imagens de inicialização não usadas**: imagens de inicialização não referenciadas para uso de sequência de tarefas ou inicialização PXE. Para obter mais informações, consulte [Gerenciar imagens de inicialização](/sccm/osd/get-started/manage-boot-images).  

- **Itens de configuração não usados**: itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias. Para obter mais informações, consulte [Criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).  


### <a name="security"></a>Segurança
Insights para melhorar a segurança dos dispositivos e da infraestrutura. 

- **Versões de cliente antimalware sem suporte**: mais de 10% dos clientes estão executando versões do System Center Endpoint Protection que não têm suporte. Para obter mais informações, confira [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Gerenciamento simplificado

Insights que ajudam você a simplificar o gerenciamento diário do seu ambiente. 

- **Versões de cliente não CB**: lista todos os clientes cujas versões não são um build do CB (branch) atual. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  


### <a name="software-center"></a>Centro de software

Insights para gerenciar o Centro de Software. 

- **Direcionar os usuários para o Centro de Software e não para o Catálogo de Aplicativos**: verifique se os usuários instalaram ou solicitaram aplicativos no Catálogo de Aplicativos nos últimos 14 dias. Agora, a principal funcionalidade do Catálogo de Aplicativos está incluída no Centro de Software. O suporte ao site Catálogo de Aplicativos foi encerrado na versão 1806. Para obter mais informações, confira [Recursos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Usar a nova versão do Centro de Software**: não há mais suporte para a versão anterior do Centro de Software. Configurar clientes para usarem o novo Centro de Software habilitando a configuração do cliente **Usar o novo Centro de Software** o grupo **Agente de Computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  


### <a name="windows-10"></a>Windows 10

Insights relacionados à implantação e à manutenção do Windows 10. O grupo de insights de gerenciamento do Windows 10 está disponível apenas quando mais da metade dos clientes estão executando o Windows 7, o Windows 8 ou o Windows 8.1.

- **Configurar a telemetria do Windows e a chave de ID comercial**: para usar dados do Upgrade Readiness, configure os dispositivos com uma chave de ID comercial e habilite a telemetria. Defina os dispositivos Windows 10 para o nível de telemetria Avançado (Limitado) ou superior. Para obter mais informações, confira [Configurar clientes para relatar dados ao Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Conectar o Configuration Manager ao Upgrade Readiness**: utilize o Upgrade Readiness para agilizar as implantações do Windows 10 antes que o Windows 7 fique sem suporte. Para obter mais informações, confira [Integrar o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Regras de insights de gerenciamento do Windows 10
![Insights de gerenciamento – Regras do Windows 10](./media/Windows-10-insights-group.png)
