---
title: Informações de gerenciamento
titleSuffix: Configuration Manager
description: Saiba mais sobre a funcionalidade de insights de gerenciamento disponível no console do Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8621f759a2e79090c6cd6dac5f2f3749147cabed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133343"
---
# <a name="management-insights-in-configuration-manager"></a>Insights de gerenciamento no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os insights de gerenciamento do Configuration Manager fornecem informações sobre o estado atual do ambiente. As informações baseiam-se na análise de dados do banco de dados do site. As informações ajudam você a melhor compreender seu ambiente e executar ações com base nas informações. Esse recurso foi lançado no Configuration Manager versão 1802. <!--1353967-->



## <a name="review-management-insights"></a>Examinar insights de gerenciamento 

Para exibir as regras, sua conta precisa da permissão de **leitura** no objeto **site**.

1. Abra o Console do Configuration Manager.  

2. Vá para o workspace **Administração**, expanda **Insights de gerenciamento** e selecione **Todos os Insights**.  

    > [!Note]  
    > Da versão 1810 em diante, quando você seleciona o nó **Insights de Gerenciamento**, ele mostra o [Painel de insights de gerenciamento](#bkmk_insights).  

3. Abra o nome do grupo de insights de gerenciamento que você deseja examinar. Selecione **Mostrar Insights** na faixa de opções.  

As quatro guias a seguir estão disponíveis para revisão: 

- **Todas as Regras**: fornece a lista completa de regras do grupo de insight de gerenciamento escolhido.  

- **Completa**:  lista as regras que não exigem qualquer ação.  

- **Em andamento**: mostra as regras em que alguns, não todos, os pré-requisitos foram atendidos.  

- **Ação Necessária**: lista as regras que precisam de ações. Selecione **Mais Detalhes** para recuperar itens específicos nos quais uma ação é necessária.  

O painel **Pré-requisitos** lista os itens necessários para executar a regra.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas as regras e os pré-requisitos do grupo de serviços de nuvem
![Insights de gerenciamento – Todas as regras e os pré-requisitos do grupo de serviços de nuvem](./media/Management-insights-all-cloud-rules.png)


Selecione uma regra e, em seguida, selecione **Mais Detalhes** para ver os detalhes da regra.



## <a name="operations"></a>Operações

As regras dos insights de gerenciamento reavaliam sua aplicabilidade de acordo com um agendamento semanal. Para reavaliar uma regra sob demanda, clique com o botão direito do mouse na regra e selecione **Reavaliar**.

O arquivo de log das regras de insight de gerenciamento está em **SMS_DataEngine.log** no servidor do site.

<!--1357930--> Começando na versão 1806, algumas regras permitem executar uma ação. Selecione uma regra, selecione **Mais Detalhes** e, se disponível, selecione **Agir**. 

Dependendo da regra, essa ação tem um dos seguintes comportamentos:  

- Navegar automaticamente no console até o nó, onde você pode realizar outras ações. Por exemplo, se a percepção do gerenciamento recomenda alterar uma configuração de cliente, a ação leva para o nó Configurações do Cliente. Em seguida, execute outras ações modificando o objeto de configurações do cliente padrão ou personalizadas.  

- Navegar para uma visualização filtrada com base em uma consulta. Por exemplo, a ação na regra de coleções vazias mostra apenas essas coleções na lista de coleções. Em seguida, execute outras ações, como excluir uma coleção ou modificar suas regras de associação.  



## <a name="bkmk_insights"></a> Painel de insights de gerenciamento
<!--1357979-->

Da versão 1810 em diante, o nó **Insights de Gerenciamento** inclui um painel gráfico. Esse painel exibe uma visão geral dos estados de regra, que torna mais fácil mostrar seu progresso. 

Use os filtros a seguir na parte superior do painel para refinar a exibição:
- Mostrar concluído
- Opcional
- Recomendado
- Crítico

O painel inclui os seguintes blocos:  

- **Índice de insights de gerenciamento**: Rastreia o progresso geral nas regras de insights de gerenciamento. O índice é uma média ponderada. As regras críticas valem o máximo. Esse índice dá o menor peso às regras opcionais.  

- **Grupos de insights de gerenciamento**: mostra o percentual de regras em cada grupo, respeitando os filtros. Selecione um grupo para fazer drill down das regras específicas neste grupo.  

- **Prioridade de insights de gerenciamento**: mostra o percentual de regras por prioridade, respeitando os filtros.   

- **Todos os insights**: Uma tabela de insights incluindo a prioridade e o estado. Use o campo **Filtro** na parte superior da tabela para coincidir com cadeias de caracteres em qualquer uma das colunas disponíveis. O painel classifica a tabela na seguinte ordem:
    - Status: Ação Necessária, Completa, Desconhecido  
    - Prioridade: Crítica, Recomendada, Opcional  
    - Última Alteração: datas mais antigas na parte superior   

![Captura de tela do painel de insights de gerenciamento](media/1357979-management-insights-dashboard.png)



## <a name="groups-and-rules"></a>Grupos e regras

As regras são organizadas nos seguintes grupos de insight de gerenciamento:
- [Aplicativos](#applications)  
- [Serviços de nuvem](#cloud-services)  
- [Coleções](#collections)  
- [Manutenção proativa](#proactive-maintenance)  
- [Security](#security)  
- [Gerenciamento simplificado](#simplified-management)  
- [Centro de Software](#software-center)  
- [Windows 10](#windows-10)  


### <a name="applications"></a>Aplicativos

Insights do gerenciamento de aplicativos.

- **Aplicativos sem implantações**: Lista os aplicativos no ambiente que não tem implantações ativas. Essa regra ajuda você a encontrar e excluir aplicativos não utilizados para simplificar a lista de aplicativos exibidos no console. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).  


### <a name="cloud-services"></a>Serviços de Nuvem

Ajuda você a integrar vários serviços de nuvem, o que permite o gerenciamento moderno de seus dispositivos. 

- **Avaliar a preparação do cogerenciamento**: ajuda você a entender quais etapas são necessárias para habilitar o cogerenciamento. Essa regra tem pré-requisitos. Para obter mais informações, confira [Visão geral do cogerenciamento](/sccm/comanage/overview).  

- **Configurar serviços do Azure para uso com o Configuration Manager**: essa regra ajuda você a integrar o Configuration Manager ao Azure AD, o que permite que os clientes se autentiquem no site usando o Azure AD. Para obter mais informações, consulte [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Habilitar os dispositivos a ingressarem no Azure Active Directory híbrido**: os dispositivos que ingressaram no Azure AD permitem que os usuários entrem com suas credenciais de domínio, o que garante que os dispositivos atendam aos padrões de segurança e conformidade da organização. Para obter mais informações, confira [Considerações de design de identidade do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Atualizar clientes para a versão mais recente do Windows 10**: o Windows 10, versão 1709 ou acima, melhora e moderniza a experiência de computação dos usuários. Para obter mais informações, confira [Principais artigos sobre a adoção do Windows como serviço](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Coleções

Insights que ajudam a simplificam o gerenciamento limpando e reconfigurando coleções.

- **Coleções vazias**: lista coleções em seu ambiente que não têm membros. Para obter mais informações, confira [Como gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections).  


### <a name="proactive-maintenance"></a>Manutenção proativa
<!--1352184--> Começando na versão 1806, as regras deste grupo destacam possíveis problemas de configuração que podem ser evitados por meio da manutenção dos objetos do Configuration Manager.    

- **Grupos de limites sem sistemas de sites atribuídos**: sem sistemas de sites atribuídos, os grupos de limites só podem ser usados para atribuição de site. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Grupos de limites sem membros**: grupos de limites não serão aplicáveis para a pesquisa de conteúdo ou a atribuição de site se não tiverem membros. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Pontos de distribuição que não fornecem conteúdo a clientes**: pontos de distribuição que não forneceram conteúdo aos clientes nos últimos 30 dias. Esses dados se baseiam nos relatórios de clientes de seu histórico de download. Para obter mais informações, consulte [Instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Habilitar limpeza do WSUS**: verifica se você habilitou a opção para executar a limpeza do WSUS nas propriedades do componente de ponto de atualização de software. Essa opção ajuda a melhorar o desempenho do WSUS. Para obter mais informações, confira [Manutenção de atualização de software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Imagens de inicialização não usadas**: imagens de inicialização não referenciadas para uso em sequência de tarefas ou inicialização PXE. Para obter mais informações, consulte [Gerenciar imagens de inicialização](/sccm/osd/get-started/manage-boot-images).  

- **Itens de configuração não usados**: itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias. Para obter mais informações, consulte [Criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Atualizar origens de cache par para a versão mais recente do cliente do Configuration Manager**: identifique clientes que servem como uma origem do cache par, mas não foram atualizados de uma versão de cliente anterior à 1806. Os clientes anteriores à 1806 não podem ser usados ​​como uma origem do cache par para clientes que executam a versão 1806 ou posterior. Selecione **Executar ação** para abrir um modo de exibição de dispositivo que exiba a lista de clientes.<!--1358008-->  


### <a name="security"></a>Segurança
Insights para melhorar a segurança dos dispositivos e da infraestrutura. 

- **Versões do cliente de antimalware sem suporte**: mais de 10% dos clientes estão executando versões do System Center Endpoint Protection que não têm mais suporte. Para obter mais informações, confira [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Gerenciamento simplificado

Insights que ajudam você a simplificar o gerenciamento diário do seu ambiente. 

- **Versões de cliente não CB**: lista todos os clientes cujas versões não são um build do branch atual. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  


### <a name="software-center"></a>Centro de software

Insights para gerenciar o Centro de Software. 

- **Direcionar os usuários para o Centro de Software em vez de para o Catálogo de Aplicativos**: verifique se os usuários instalaram ou solicitaram aplicativos do Catálogo de Aplicativos nos últimos 14 dias. Agora, a principal funcionalidade do Catálogo de Aplicativos está incluída no Centro de Software. O suporte ao site Catálogo de Aplicativos foi encerrado na versão 1806. Para obter mais informações, confira [Recursos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Usar a nova versão do Centro de Software**: A versão anterior do Centro de Software não tem mais suporte. Configurar clientes para usarem o novo Centro de Software habilitando a configuração do cliente **Usar o novo Centro de Software** o grupo **Agente de Computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  


### <a name="windows-10"></a>Windows 10

Insights relacionados à implantação e à manutenção do Windows 10. O grupo de insights de gerenciamento do Windows 10 está disponível apenas quando mais da metade dos clientes estão executando o Windows 7, o Windows 8 ou o Windows 8.1.

- **Configurar a telemetria do Windows e a chave de ID comercial**: para usar dados do Upgrade Readiness, configure os dispositivos com uma chave de ID Comercial e habilite a telemetria. Defina os dispositivos Windows 10 para o nível de telemetria Avançado (Limitado) ou superior. Para obter mais informações, confira [Configurar clientes para relatar dados ao Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Conectar o Configuration Manager ao Upgrade Readiness**: utilize o Upgrade Readiness para agilizar as implantações do Windows 10 antes que o Windows 7 fique sem suporte. Para obter mais informações, confira [Integrar o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Regras de insights de gerenciamento do Windows 10
![Insights de gerenciamento – Regras do Windows 10](./media/Windows-10-insights-group.png)
