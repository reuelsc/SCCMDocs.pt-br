---
title: Novidades na versão 1810
titleSuffix: Configuration Manager
description: Obtenha os detalhes sobre as alterações e as novas funcionalidades introduzidas na versão 1810 do branch atual do Configuration Manager.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d2ab324038e833da7bc080286c820b3df8d06fa
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558160"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Novidades na versão 1810 do branch atual do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização do 1810 para o branch atual do Configuration Manager está disponível como uma atualização no console. Aplique essa atualização em sites que executam a versão 1710, 1802 ou 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> Este artigo resume as alterações e os novos recursos no Configuration Manager, versão 1810.  

Sempre examine a lista de verificação mais recente para instalar essa atualização. Para obter mais informações, confira [Lista de verificação para instalar a atualização 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). Depois de atualizar um site, examine também a [Lista de verificação pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

Para aproveitar os novos recursos do Configuration Manager, primeiro atualize os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.

> [!Note]  
> Atualmente, esse artigo lista todos os recursos importantes nesta versão. No entanto, nem todas as seções ainda se vinculam ao conteúdo atualizado com informações adicionais sobre os novos recursos. Continue verificando esta página regularmente para ver se há atualizações. As alterações são indicadas com a marcação ***[Atualizado]***. Essa observação será removida quando o conteúdo for finalizado.  

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole a seguinte URL em seu leitor de feeds de RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a> Sistemas operacionais e recursos preteridos

Saiba mais sobre alterações de suporte antes que elas sejam implementadas em [itens removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A partir de 14 de agosto de 2018, o recurso de gerenciamento de dispositivo móvel híbrido foi preterido. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

O suporte do SCEP (System Center Endpoint Protection) para Mac e Linux (todas as versões) será encerrado em 31 de dezembro de 2018. A disponibilidade de novas definições de vírus do SCEP para Mac e do SCEP para Linux poderá ser descontinuada após o encerramento do suporte. Para obter mais informações, consulte a [postagem no blog sobre o encerramento do suporte](https://go.microsoft.com/fwlink/?linkid=870182).

Implantações de serviço clássico no Azure agora são preteridas no Configuration Manager. Comece a usar as implantações do Azure Resource Manager para o gateway de gerenciamento de nuvem e o ponto de distribuição de nuvem. Para obter mais informações, confira [Planejar para CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a> Infraestrutura do site

### <a name="support-for-windows-server-2019"></a>Suporte para Windows Server de 2019
<!--1359195--> O Configuration Manager agora dá suporte ao Windows Server 2019 e ao Windows Server versão 1809 como sistemas de sites. 

Para obter mais informações, confira [Sistemas operacionais com suporte para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Suporte de hierarquia para alta disponibilidade do servidor de site
<!--1358224--> Sites de administração central e sites primários filho agora podem ter um servidor de site adicional no modo passivo. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>Melhorias aos pré-requisitos de instalação

Quando você instala ou atualiza para a versão 1810, a instalação do Configuration Manager agora inclui ou melhora as verificações de pré-requisitos a seguir:

- **Reinicialização do sistema pendente**: Essa verificação de pré-requisitos agora é mais resiliente. Ela verifica as chaves de Registro adicionais para recursos do Windows. Para obter mais informações, confira [Reinicialização do sistema pendente](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Limpeza do controle de alterações do SQL**: Verificar novamente se o banco de dados do site tem uma lista de pendências de dados de controle de alterações do SQL. Para obter mais informações, incluindo um procedimento para verificar e limpar a lista de pendências, confira [Limpeza do controle de alterações do SQL](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Versão do SQL Native Client**: Essa verificação de pré-requisito é atualizada para versões do SQL Native Client que dão suporte a TLS 1.2. A versão mínima é [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Para obter mais informações, confira a [versão do SQL Native Client](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Sistema de sites no nó de cluster do Windows**: O processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. O Always On do SQL requer essa função; portanto, anteriormente não era possível colocar o banco de dados do site no servidor do site. Com essa alteração, é possível criar um site altamente disponível com menos servidores usando o Always On do SQL e um servidor do site no modo passivo. Para obter mais informações, confira [Cluster de failover do Windows](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>Nova permissão para ações de notificação do cliente
<!--SCCMDocs-pr issue #2972--> Ações de notificação do cliente agora exigem a permissão **Notificar Recurso** na classe SMS_Collection. As seguintes funções internas têm esta permissão por padrão:
- Administrador Completo  
- Administrador de Infraestrutura  

Adicione essa permissão a quaisquer funções personalizadas que precisam usar ações de notificação do cliente. 

Para obter mais informações, confira [Notificações do cliente](/sccm/core/clients/manage/client-notification).



## <a name="bkmk_content"></a> Gerenciamento de conteúdo

### <a name="new-boundary-group-options"></a>Novas opções do novo grupo de limites
<!--1358749--> Os grupos de limites agora incluem as seguintes configurações adicionais para dar a você mais controle sobre a distribuição de conteúdo em seu ambiente:

- **Preferir pontos de distribuição a de pares na mesma sub-rede**: Por padrão, o ponto de gerenciamento prioriza as fontes de cache par na parte superior da lista de locais de conteúdo. Essa configuração reverte essa prioridade para clientes que estão na mesma sub-rede que a fonte de cache par.  

- **Preferir a pontos de distribuição em nuvem a pontos de distribuição**: Se você tiver uma filial com um link da Internet mais rápido, poderá priorizar o conteúdo de nuvem.  

Para saber mais, confira [Opções de grupo de limites para downloads de pares](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regra de insights de gerenciamento para a versão do cliente da origem do cache par
<!-- 1358008 --> O nó **Insights de Gerenciamento** têm uma nova regra para identificar clientes que servem como uma origem do cache par, mas não fizeram upgrade de uma versão de cliente anterior à 1806. A nova regra é **Atualizar fontes de cache par para a versão mais recente do cliente Configuration Manager** e faz parte do novo grupo de regras **Manutenção Proativa**. Os clientes anteriores à 1806 não podem ser usados ​​como uma origem do cache par para clientes que executam a versão 1806 ou posterior. Selecione **Executar ação** para abrir um modo de exibição de dispositivo que exiba a lista de clientes. 

Para obter mais informações, veja [Insights de gerenciamento](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Gerenciamento de cliente

### <a name="new-client-notification-action-to-wake-up-device"></a>Nova ação de notificação de cliente para ativação de dispositivo
<!--1317364--> Agora é possível ativar clientes no console do Configuration Manager, mesmo se o cliente não está na mesma sub-rede que o servidor do site. Se precisar realizar manutenção ou consultar dispositivos, você não estará limitado por clientes remotos que estão em suspensão. O servidor do site usa o canal de notificação do cliente para identificar o outro cliente que está ativo na mesma sub-rede remota. O cliente ativo então envia uma solicitação Wake On LAN (Magic Packet).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nova opção para executar a notificação de cliente em nó de dispositivos
<!--1317364--> Até a versão 1810, a opção **Notificação de Cliente** só estava disponível no nó Coleção de Dispositivos ou ao exibir a associação de uma Coleção de Dispositivos. Agora é possível executar uma **Notificação de Cliente** diretamente no nó **Dispositivos**. Não é mais necessário estar dentro de uma exibição de associação de coleção. 

Para obter mais informações, confira [Notificações do cliente](/sccm/core/clients/manage/client-notification).


### <a name="improvements-to-collection-evaluation"></a>Melhorias à avaliação de coleção
<!--3607726, fka 1358981-->
 ***[ATUALIZADO]*** As seguintes alterações no comportamento de avaliação de coleção podem melhorar o desempenho do site:  

- Anteriormente, quando você configurava um agendamento em uma coleção baseada em consulta, o site continuava a avaliar a consulta, independentemente de você ter ativado ou não a configuração de coleção para **Agendar uma atualização completa nesta coleção**. Para desabilitar totalmente o agendamento, era preciso alterá-lo para **Nenhum**. Agora o site remove o agendamento ao desabilitar essa configuração. Para especificar um agendamento para avaliação de coleção, ative a opção **Agendar uma atualização completa nesta coleção**.  

- Você não pode desabilitar a avaliação de coleções internas como **Todos os sistemas**, mas agora pode configurar o agendamento. Esse comportamento permite que você personalize essa ação em um momento que atenda aos seus requisitos de negócios. 

Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections#bkmk_create).


### <a name="improvement-to-client-installation"></a>Melhoria à instalação do cliente
<!--1358840--> Ao instalar o cliente do Configuration Manager, o processo ccmsetup contata o ponto de gerenciamento para localizar o conteúdo necessário. Anteriormente neste processo, o ponto de gerenciamento só retorna pontos de distribuição no grupo de limites atuais do cliente. Se nenhum conteúdo estiver disponível, o processo de instalação regredirá para baixar o conteúdo do ponto de gerenciamento. Não há nenhuma opção de regredir para os pontos de distribuição em outros grupos de limites que podem ter o conteúdo necessário. Agora, o ponto de gerenciamento retorna pontos de distribuição com base na configuração do grupo de limites. 

Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).



## <a name="bkmk_comgmt"></a> Cogerenciamento

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Política de conformidade de aplicativo necessária para dispositivos cogerenciados
<!--1358196--> Defina regras de política de conformidade no Configuration Manager para os aplicativos necessários. Essa avaliação de aplicativo faz parte do estado de conformidade geral enviado para o Microsoft Intune para dispositivos cogerenciados.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>Melhoria ao painel de cogerenciamento
<!--1358980--> O painel de cogerenciamento foi aprimorado com as seguintes informações mais detalhadas:  

- O bloco **Status do registro de cogerenciamento** inclui estados adicionais

- Um novo bloco **Status de cogerenciamento** com um gráfico de funil que mostra os estados do processo de registro

- Um novo bloco com contagens de **Erros de registro**

![Captura de tela do painel de cogerenciamento mostrando os quatro blocos principais](media/1358980-comgmt-dashboard.png)

Para obter mais informações, confira [Painel de cogerenciamento](/sccm/comanage/how-to-monitor#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Melhorias à configuração de clientes baseados na Internet
<!--3607731, fka 1359181-->
 ***[ATUALIZADO]*** Esta versão simplifica ainda mais o processo de configuração de cliente do Configuration Manager para clientes na Internet. O site publica informações adicionais do Azure AD (Azure Active Directory) no gateway de gerenciamento de nuvem (CMG). Um cliente associado ao Azure AD obtém essas informações do CMG durante o processo ccmsetup, usando o mesmo locatário ao qual ele está associado. Esse comportamento simplifica ainda mais o registro de dispositivos para o cogerenciamento em um ambiente com mais de um locatário do Azure AD. Agora as duas únicas propriedades necessárias do ccmsetup são **CCMHOSTNAME** e **SMSSiteCode**.

Para saber mais, consulte [Como preparar dispositivos baseados na Internet para cogerenciamento](/sccm/comanage/how-to-prepare-Win10#install-the-configuration-manager-client).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gerenciamento de aplicativos

### <a name="convert-applications-to-msix"></a>Converter aplicativos em MSIX
<!--3607729, fka 1359029-->
 ***[Atualizado]*** A partir da versão 1806, o Configuration Manager dá suporte à implantação do novo formato de pacote de aplicativo (.msix) do Windows 10. Agora você pode converter seus aplicativos existentes do Windows Installer (.msi) para o formato MSIX.

Para obter mais informações, confira [Criar aplicativos Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_msix).  


### <a name="repair-applications"></a>Reparar aplicativos
<!--1357866--> Especifique uma linha de comando de reparo para tipos de implantação do Windows Installer e do Instalador de Script. Se você habilitar a opção na implantação, um novo botão estará disponível no Centro de Software para **Reparo** do aplicativo. Ao configurar um aplicativo com um programa de reparo, os usuários podem iniciar o comando no Centro de Software. 

Para obter mais informações, confira [Criar aplicativos](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) e [Implantar aplicativos](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Aprovar solicitações de aplicativo por email
<!--1321550--> Configure notificações por email para solicitações de aprovação do aplicativo. Quando um usuário solicitar um aplicativo, você receberá um email. Clique nos links no email para aprovar ou negar a solicitação sem precisar usar o console do Configuration Manager.

Para obter mais informações, confira [Aprovar aplicativos](/sccm/apps/deploy-use/app-approval).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Métodos de detecção não carregam perfis do Windows PowerShell
<!--3607762, fka 1359239-->
 ***[ATUALIZADO]*** Você pode usar scripts do Windows PowerShell para métodos de detecção em aplicativos e configurações nos itens de configuração. Agora, quando esses scripts são executados em clientes, o cliente do Configuration Manager chama o PowerShell com o parâmetro `-NoProfile`. Essa opção inicia o PowerShell sem perfis. 

Um perfil do PowerShell é um script executado quando o PowerShell é iniciado. Você pode criar um perfil do PowerShell para personalizar seu ambiente e adicionar elementos específicos da sessão para cada sessão do PowerShell que você iniciar. 

> [!Note]  
> Essa alteração no comportamento não se aplica a [Scripts](/sccm/apps/deploy-use/create-deploy-scripts) ou [CMPivot](/sccm/core/servers/manage/cmpivot). Ambos os recursos já usam esse parâmetro do PowerShell.    

Para obter mais informações, confira [Criar aplicativos](/sccm/apps/deploy-use/create-applications) e [Criar itens de configuração personalizados](/sccm/compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client).



## <a name="bkmk_osd"></a> Implantação do sistema operacional

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Suporte à sequência de tarefas do Windows Autopilot para dispositivos existentes
<!--3607717, fka 1358333-->

***[Atualizado]*** O [Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está agora disponível com o Windows 10, versão 1809 ou posterior. Esse novo recurso permite refazer a imagem e provisionar um dispositivo Windows 7 para o [modo orientado pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando uma única sequência de tarefas nativa do Configuration Manager. 

Para saber mais, confira [Windows Autopilot para dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Especifique a unidade para manutenção offline da imagem do sistema operacional  
<!--1358924--> Agora, especifique a unidade que usa o Configuration Manager ao adicionar atualizações de software às imagens do sistema operacional e aos pacotes de atualização do sistema operacional. Esse processo pode consumir uma grande quantidade de espaço em disco com arquivos temporários, portanto, essa opção oferece flexibilidade na escolha da unidade que será usada. 

Para obter mais informações, confira [Gerenciar imagens do sistema operacional](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) ou [Gerenciar pacotes de atualização do sistema operacional](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Suporte à sequência de tarefas para grupos de limites
<!--1359025--> Quando um dispositivo executa uma sequência de tarefas e precisa adquirir conteúdo, agora ele usa comportamentos de grupo de limites semelhantes ao cliente do Configuration Manager.   

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Melhorias na manutenção do driver
<!--3607716, fka 1358270-->
 ***[Atualizado]*** Agora os pacotes de driver têm mais campos de metadados para **Fabricante** e **Modelo**. Use esses campos para marcar pacotes de driver com informações para auxiliar na manutenção geral do sistema ou para identificar drivers antigos e duplicados que podem ser excluídos.

Para mais informações, consulte [Manage drivers (Gerenciar drivers)](/sccm/osd/get-started/manage-drivers).


### <a name="new-task-sequence-variable-for-last-action-name"></a>Nova variável de sequência de tarefas para o nome da última ação
<!--SCCMDocs-pr issue #2964--> Juntamente com a variável de sequência de tarefas _SMSTSLastActionRetCode, a sequência de tarefas também define uma nova variável **_SMSTSLastActionName**. Também registra esse valor para o arquivo smsts.log. Essa nova variável é útil ao solucionar problemas de uma sequência de tarefas. Quando uma etapa falha, um script personalizado pode incluir o nome da etapa junto com o código de retorno.

Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a> Atualizações de software

### <a name="phased-deployment-of-software-updates"></a>Implantação em fases de atualizações de software
<!--1358146--> Criar implantações em fases para atualizações de software. As implantações em fases permitem que você coordene uma distribuição coordenada e sequenciada do software com base em grupos e critérios personalizáveis.

Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Melhoria de janelas de manutenção para atualizações de software
<!--vso2839307--> A seguinte configuração do cliente está no grupo **Atualizações de Software** para controlar o comportamento da instalação de atualizações de software em janelas de manutenção: 

**Permitir a instalação de atualizações na janela de manutenção "Todas as implantações" quando a janela de manutenção "Atualização de software" estiver disponível**

Por padrão, essa opção é **Não** para manter a consistência com o comportamento existente. Altere-a para **Sim** para permitir que os clientes usem outras janelas de manutenção disponíveis para instalar atualizações de software.

<!--For more information, see []().-->

### <a name="improvement-to-software-updates-maintenance"></a>Melhoria na manutenção de atualizações de software
<!--2839349--> As tarefas de limpeza do WSUS agora são executadas em sites secundários. As atualizações expiradas de limpeza do WSUS são executadas e as atualizações substituídas são recusadas no WSUS para sites secundários.

Para obter mais informações, veja [Comportamento de limpeza do WSUS começando na versão 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810)

## <a name="bkmk_report"></a> Relatórios

### <a name="improvement-to-lifecycle-dashboard"></a>Melhoria ao painel do ciclo de vida
<!--1358702--> O painel de ciclo de vida do produto agora inclui informações para **System Center 2012 Configuration Manager e versões posteriores**. 

Também há um novo relatório, **Ciclo de vida 05A – painel de ciclo de vida do produto**. Inclui informações semelhantes como o painel no console.

Para obter mais informações sobre esse painel, confira [Usar o painel do ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="improvement-to-data-warehouse"></a>Melhoria ao data warehouse
<!--1358870--> Agora você pode sincronizar mais tabelas do banco de dados do site para o data warehouse. Essa alteração permite que você crie mais relatórios com base nas necessidades empresariais.

Para obter mais informações, confira [Data warehouse](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Console do Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Autenticação de administrador do Configuration Manager
<!--1357013--> Agora você pode especificar o nível mínimo de autenticação para os administradores acessarem sites do Configuration Manager. Esse recurso faz com que os administradores entrem no Windows com o nível necessário. Para definir essa configuração, localize a guia **Autenticação** em **Configurações de Hierarquia**. 

Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth).


### <a name="support-center"></a>Centro de Suporte
<!--1357489--> Use o Centro de Suporte para solução de problemas do cliente, exibição de log em tempo real ou captura do estado de um computador de cliente do Configuration Manager para análise posterior. O Centro de Suporte é uma ferramenta única para combinar diversas ferramentas de solução de problemas do administrador. Localize o instalador do Centro de Suporte no servidor do site na pasta **cd.latest\SMSSETUP\Tools\SupportCenter**.

Para obter mais informações, confira [Centro de Suporte](/sccm/core/support/support-center).


### <a name="management-insights-dashboard"></a>Painel de insights de gerenciamento
<!--1357979-->

O nó **Insights de gerenciamento** agora inclui um painel gráfico. Esse painel exibe uma visão geral dos estados de regra, que torna mais fácil mostrar seu progresso. O painel inclui os seguintes blocos:

- **Índice de insights de gerenciamento**: Rastreia o progresso geral nas regras de insights de gerenciamento. O índice é uma média ponderada. As regras críticas valem o máximo. Esse índice dá o menor peso às regras opcionais.  

- **Grupos de insights de gerenciamento**: Mostra o percentual de regras em cada grupo.  

- **Prioridade de insights de gerenciamento**: Mostra o percentual de regras por prioridade.  

- **Todos os insights**: Uma tabela de insights incluindo a prioridade e o estado.  

![Captura de tela do painel de insights de gerenciamento](media/1357979-management-insights-dashboard.png)

Para obter mais informações, veja [Insights de gerenciamento](/sccm/core/servers/manage/management-insights).


### <a name="improvements-to-cmpivot"></a>Melhorias ao CMPivot
<!--1359068--> O CMPivot inclui os seguintes aprimoramentos:

- Salvar consultas **favoritas**  

- Na guia Resumo da Consulta, selecione a contagem de dispositivos com falha e offline e, em seguida, selecione a opção para **Criar coleção**. 

Para obter mais informações sobre outras melhorias no desempenho e na solução de problemas do CMPivot, confira [Melhorias nos scripts](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Melhorias nos scripts
<!--1358239--> Agora você pode exibir a saída detalhada do script em formato JSON bruto ou estruturado. Essa formatação facilita a leitura e a análise da saída. 

As melhorias na solução de problemas e no desempenho a seguir aplicam-se ao CMPivot e aos scripts:

- Os clientes atualizados retornam uma saída menor do que 80 KB para o site por meio de um canal de comunicação rápido. Essa alteração aumenta o desempenho da exibição da saída do script ou da consulta.  

- Logs adicionais para solução de problemas  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>API do Provedor de SMS
<!--1321523--> O Provedor de SMS agora fornece acesso de interoperabilidade da API somente leitura ao WMI por HTTPS. O **Provedor de SMS** aparece como uma função com uma opção para permitir a comunicação pelo gateway de gerenciamento de nuvem. O uso atual para essa configuração é habilitar as aprovações de aplicativo por email de um dispositivo remoto. Para obter mais informações, confira [Aprovar solicitações de aplicativos por email](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> MDM local

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Uma conexão do Intune não é mais necessária para novas implantações do MDM local
<!--1359124--> O pré-requisito do MDM local para configurar uma assinatura do Microsoft Intune não é mais necessária para novas implantações. Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, é possível remover a conexão do Intune das implantações de MDM locais existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Outras atualizações

Além de novos recursos, este lançamento inclui outras alterações, como correções de bugs. Para obter mais informações, confira [Resumo das alterações no Branch Atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4482169).

Para saber mais sobre alterações nos cmdlets do Windows PowerShell para Configuration Manager, confira [Notas sobre a versão 1810 do PowerShell](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

O seguinte pacote cumulativo de atualizações (4486457) foi disponibilizado no console em 25 de janeiro de 2019: [Pacote cumulativo de atualizações do branch atual do Configuration Manager, versão 1810](https://support.microsoft.com/help/4486457).


### <a name="hotfixes"></a>Hotfixes

Os seguintes hotfixes adicionais estão disponíveis para resolver problemas específicos:

| ID | Título | Data | No console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | O certificado do conector do Microsoft Intune não é renovado no Configuration Manager | 18 de janeiro de 2019 | Sim |
| [4490434](https://support.microsoft.com/help/4490434) | As colunas de descoberta de usuário duplicado são criadas no Configuration Manager | 22 de fevereiro de 2019 | Sim |
| [4490575](https://support.microsoft.com/help/4490575) | As instalações de atualização param de responder ou nunca mostram a conclusão no Configuration Manager, versão 1810 | 22 de fevereiro de 2019 | Sim |


## <a name="next-steps"></a>Próximas etapas

Quando estiver pronto para instalar esta versão, confira [Instalação de atualizações para o Configuration Manager](/sccm/core/servers/manage/updates) e [Lista de verificação para instalação da atualização 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> Para instalar um novo site, use uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalação de novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para problemas conhecidos e significativos, veja [Notas de versão](/sccm/core/servers/deploy/install/release-notes).

Depois de atualizar um site, examine também a [Lista de verificação pós-atualização](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).
