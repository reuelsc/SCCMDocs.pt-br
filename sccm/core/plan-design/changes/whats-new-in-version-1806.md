---
title: Novidades na versão 1806
titleSuffix: Configuration Manager
description: Obtenha os detalhes sobre as alterações e as novas funcionalidades introduzidas na versão 1806 do branch atual do Configuration Manager.
ms.date: 07/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c6ae28a50f3145420895b295ebe730fb7b2a9a7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386057"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Novidades na versão 1806 do branch atual do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização do 1806 para o branch atual do Configuration Manager está disponível como uma atualização no console. Aplique essa atualização em sites que executam a versão 1706, 1710 ou 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

> [!Important]  
> Atualmente, esse artigo lista todos os recursos importantes nesta versão. No entanto, nem todas as seções ainda se vinculam ao conteúdo atualizado com informações adicionais sobre os novos recursos. Continue verificando esta página regularmente para ver se há atualizações. As alterações são indicadas com a marcação ***[Atualizado]***. Essa observação será removida quando o conteúdo for finalizado.  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


As seções a seguir apresentam detalhes sobre as alterações e os novos recurso introduzidos na versão 1806 do branch atual do Configuration Manager.  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="cmpivot"></a>CMPivot
<!--1358456--> O Configuration Manager sempre forneceu um grande armazenamento centralizado de dados do dispositivo, que os clientes usam para fins de relatório. O site normalmente coleta esses dados semanalmente. O CMPivot é um novo utilitário no console que dá acesso ao estado dos em tempo real dos dispositivos no seu ambiente. Ele executa imediatamente uma consulta em todos os dispositivos atualmente conectados na coleção de destino e retorna os resultados. Você pode então filtrar e agrupar esses dados na ferramenta. Ao fornecer dados em tempo real de clientes online, você pode responder a perguntas de negócios com mais rapidez, solucionar problemas e responder a incidentes de segurança. 

Para obter mais informações, veja [CMPivot](/sccm/core/servers/manage/cmpivot).  


### <a name="site-server-high-availability"></a>Alta disponibilidade do servidor do site
<!--1128774--> Alta disponibilidade para uma função de servidor do site primário é uma solução com base no Configuration Manager para instalar um servidor do site adicional no modo passivo. O servidor do site no modo passivo é usado além do servidor do site existente que está no modo ativo. Um servidor do site no modo passivo está disponível para uso imediato quando for necessário. 

Para obter mais informações, consulte os seguintes artigos: 
- [Alta disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Fluxograma – configurar um servidor do site no modo passivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Fluxograma – Promover o servidor do site (planejado)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Fluxograma – Promover o servidor do site (não planejado)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>Melhorias a insights de gerenciamento
Esta versão inclui as seguintes melhorias a insights de gerenciamento:  

- Alguns insights de gerenciamento agora têm a opção de executar uma ação. Essa ação é navegar até o nó associado no console ou mostrar uma exibição filtrada com base em consulta.<!--1357930-->  

- Um novo grupo para manutenção proativa está disponível com seis novas regras, que ajudam a realçar os possíveis problemas de configuração a evitar por meio de manutenção regular.<!--1352184-->  

Para obter mais informações, veja [Insights de gerenciamento](/sccm/core/servers/manage/management-insights).


### <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager
<!--1357145--> As ferramentas de servidor e cliente do Configuration Manager agora estão incluídas no servidor. Encontre-as na pasta `CD.Latest\SMSSETUP\Tools` no servidor do site. Nenhuma instalação adicional é necessária. 

Para obter mais informações, veja [Ferramentas do Configuration Manager](/sccm/core/support/tools).


### <a name="exclude-active-directory-containers-from-discovery"></a>Excluir contêineres do Active Directory da descoberta
<!--1358143--> Para reduzir o número de objetos descobertos, exclua contêineres específicos da descoberta do sistema do Active Directory. 



## <a name="content-management"></a>Gerenciamento de conteúdo

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurar uma biblioteca de conteúdo remoto para o servidor do site
<!--1357525--> Para configurar a alta disponibilidade do servidor do site ou para liberar espaço no disco rígido em sua administração central ou em servidores do site primário, realoque a biblioteca de conteúdo para outro local de armazenamento. Mova a biblioteca de conteúdo para outra unidade no servidor do site, para um servidor separado ou para discos tolerantes a falhas em uma rede SAN (rede de área de armazenamento). 

Para obter mais informações, consulte os seguintes artigos: 
- [Biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library)
- [Fluxograma – Gerenciar biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte a ponto de distribuição na nuvem para o Azure Resource Manager
<!--1322209--> Ao criar um ponto de distribuição na nuvem, o assistente agora oferece a opção de criar uma **implantação do Azure Resource Manager**. O Azure Resource Manager é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado grupo de recursos. Ao implantar o ponto de distribuição na nuvem com o Azure Resource Manager, o site usa o Azure AD (Azure Active Directory) para autenticar e criar os recursos necessários para a nuvem. Essa implantação modernizada não exige o certificado de gerenciamento do Azure clássico. 

A documentação do recurso para o ponto de distribuição na nuvem também foi revisada e aprimorada. Para obter mais informações, consulte os seguintes artigos:
- [Usar um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [Instalar um ponto de distribuição na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Os pontos de distribuição por pull são compatíveis com os pontos de distribuição de nuvem como origem  
<!--1321554--> Muitos clientes usam pontos de distribuição por pull em escritórios remotos ou filiais, que baixam o conteúdo de um ponto de distribuição de origem em toda a WAN. Se os escritórios remotos tiverem uma conexão melhor com a Internet ou para reduzir a carga em seus links de WAN, agora você poderá usar um ponto de distribuição na nuvem no Microsoft Azure como a origem. Quando você adiciona uma fonte na guia **Ponto de distribuição por pull** das propriedades do ponto de distribuição, qualquer ponto de distribuição de nuvem no site agora é listado como um ponto de distribuição disponível. O comportamento de ambas as funções do sistema de sites permanece o mesmo caso contrário. 

Para obter mais informações, veja [Usar um ponto de distribuição por pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Habilitar pontos de distribuição para usar o controle de congestionamento de rede
<!--1358112--> O LEDBAT (Low Extra Delay Background Transport) do Windows é um recurso do Windows Server para ajudar a gerenciar transferências de rede em segundo plano. Para pontos de distribuição em execução nas versões com suporte do Windows Server, habilite uma opção para ajudar a ajustar o tráfego da rede. Os clientes usam a largura de banda da rede somente quando ela está disponível. 

Para obter mais informações, confira [LEDBAT do Windows](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>O suporte parcial de download no cache de par de cliente para reduzir a utilização de WAN
<!--1357346--> As fontes de cache de par de cliente agora podem dividir o conteúdo em partes. Essas partes minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gerenciamento fornece acompanhamento mais detalhado das partes do conteúdo. Ele tentará eliminar mais de um download do mesmo conteúdo por grupo de limites. 

Para obter mais informações, veja [Suporte parcial a download](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Opções de grupo de limites para downloads de pares
<!--1356193--> Os grupos de limites agora incluem configurações adicionais para dar a você mais controle sobre a distribuição de conteúdo em seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir downloads de pares nesse grupo de limites**: essa configuração é habilitada por padrão. O ponto de gerenciamento fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. Essa configuração também afeta a aplicação de IDs de grupo para Otimização de Entrega.  

- **Durante downloads de pares, use apenas pares na mesma sub-rede**: essa configuração depende daquela mostrada acima. Se você habilitar essa opção, o ponto de gerenciamento incluirá apenas as origens de pares de lista do local do conteúdo que estão na mesma sub-rede que o cliente.  



<!-- ## Migration  -->



## <a name="client-management"></a>Gerenciamento de cliente

### <a name="improvement-to-client-push-security"></a>Melhoria à segurança do cliente por push
<!--1358204--> Ao usar o método de push de cliente da instalação do cliente do Configuration Manager, o site agora pode exigir a autenticação mútua do Kerberos. Essa melhoria ajuda a proteger a comunicação entre o servidor e o cliente. 

Para obter mais informações, consulte [Como instalar clientes com o push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


### <a name="bkmk_ehttp"></a> Sistema de sites HTTP aprimorado
<!--1356889,1358228--> O uso da comunicação HTTPS é recomendado para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução da integração do Azure AD (Azure Active Directory) reduz alguns, mas não todos os requisitos de certificado. 

Esta versão inclui melhorias em como os clientes se comunicam com os sistemas de sites. Nas propriedades do site, guia **Comunicação do Computador Cliente**, selecione a opção para **HTTPS ou HTTP** e, em seguida, habilite a nova opção para **Usar certificados gerados pelo Configuration Manager para sistemas de sites HTTP**. Esse recurso é um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

Essa opção é compatível com os seguintes cenários principais:  

- **Cliente para o ponto de gerenciamento HTTP**<!--1356889-->: [os dispositivos associados ao Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) podem se comunicar por meio de um CMG (Gateway de Gerenciamento de Nuvem) com um ponto de gerenciamento configurado para HTTP. O servidor do site gera um certificado para o ponto de gerenciamento, permitindo que ele se comunique por meio de um canal seguro.   

- **Ponto de distribuição de cliente para HTTP**<!--1358228-->: um cliente associado ao Azure AD ou grupo de trabalho pode baixar o conteúdo por meio de um canal seguro de um ponto de distribuição configurado para HTTP.   


### <a name="azure-ad-device-identity"></a>Identidade do dispositivo do Azure AD 
<!--1358460--> Um [dispositivo do Azure AD associado](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) ou [híbrido do Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um usuário do Azure AD conectado pode se comunicar com segurança com o site atribuído. A identidade do dispositivo baseado em nuvem agora é suficiente para autenticar com o CMG e o ponto de gerenciamento.  


### <a name="cmtrace-installed-with-client"></a>CMTrace instalado com o cliente
<!--1357971--> A ferramenta de exibição de log do CMTrace agora é instalada automaticamente junto com o cliente do Configuration Manager. Ela é adicionada ao diretório de instalação do cliente, que por padrão é `%WinDir%\ccm\cmtrace.exe`. 

Para obter mais informações, confira [CMTrace](/sccm/core/support/cmtrace).


### <a name="cloud-management-dashboard"></a>Painel de gerenciamento de nuvem
<!--1358461--> O novo painel de gerenciamento de nuvem fornece uma exibição centralizada do uso do CMG (Gateway de Gerenciamento de Nuvem). Quando o site é integrado ao Azure AD, ele também exibe dados sobre usuários e dispositivos da nuvem. No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**. Selecione o nó **Gerenciamento de Nuvem** e visualize os blocos do painel.  

Esse recurso também inclui o **Analisador de conexão CMG** para verificação em tempo real para auxiliar na solução de problemas. O utilitário no console verifica o status atual do serviço e o canal de comunicação por meio da conexão CMG aponta para os pontos de gerenciamento que permitem o tráfego CMG. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione **Gateway de Gerenciamento de Nuvem**. Selecione a instância CMG de destino e, em seguida, selecione **Analisador de conexão** na faixa de opções.


### <a name="improvements-to-cloud-management-gateway"></a>Melhorias no gateway de gerenciamento de nuvem

A versão 1806 inclui as seguintes melhorias ao CMG (Gateway de Gerenciamento de Nuvem):

#### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de inicialização de cliente simplificada
<!--1358215--> Ao instalar o cliente do Configuration Manager na Internet por meio de um CMG, a linha de comando agora requer menos propriedades. Essa melhoria reduz o tamanho da linha de comando usada no Microsoft Intune ao se preparar para o cogerenciamento. 

As propriedades de linha de comando a seguir são necessárias em todos os cenários:
  - CCMHOSTNAME  
  - SMSSITECODE  

As propriedades a seguir são necessárias ao usar o Azure AD para autenticação de cliente em vez de certificados de autenticação de cliente baseados em PKI:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

A propriedade a seguir será necessária se o cliente for retornar para a Intranet:
  - SMSMP  

O exemplo a seguir inclui todas as propriedades acima:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

<!--For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).-->

#### <a name="download-content-from-a-cmg"></a>Baixar o conteúdo de um CMG
<!--1358651--> Anteriormente, era necessário implantar um ponto de distribuição na nuvem e um CMG como funções separadas. Um CMG agora também pode fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para habilitar esse recurso, habilite a nova opção para **Permitir que o CMG funcione como um ponto de distribuição na nuvem e entregue conteúdo do armazenamento do Azure** na guia **Configurações** das propriedades do CMG. 

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>O certificado raiz confiável não é necessário com o Azure AD
<!--503899--> Ao criar um CMG, não é mais necessário fornecer um [certificado raiz confiável](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) na página Configurações. Esse certificado não é necessário ao usar o Azure AD (Azure Active Directory) para autenticação do cliente, mas costumava ser necessário no assistente. Se você estiver usando certificados de autenticação de cliente de PKI, ainda será necessário adicionar um certificado raiz confiável para o CMG.



## <a name="co-management"></a>Cogerenciamento

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizar a política de MDM do Microsoft Intune para um dispositivo cogerenciado
<!--1357377--> Quando você muda uma carga de trabalho de cogerenciamento, os dispositivos cogerenciados sincronizam a política de MDM automaticamente com o Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas Notificações do Cliente no console do Configuration Manager. 

Para obter mais informações, veja [Mudar as cargas de trabalho do Configuration Manager para o Intune](/sccm/core/clients/manage/co-management-switch-workloads).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Fazer a transição de novas cargas de trabalho para o Intune usando cogerenciamento
As cargas de trabalho a seguir agora são capazes de fazer a transição do Configuration Manager para o Intune depois de habilitar o cogerenciamento:  

- **Configuração de dispositivo**<!--1357903-->: essa carga de trabalho permite que você use o Intune para implantar políticas de MDM enquanto continua usando o Configuration Manager para implantar aplicativos.  

- **Office 365**<!--1357841-->: dispositivos não instalam as implantações do Office 365 do Configuration Manager.  

- **Aplicativos móveis**<!--1357892-->: todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software. Esse recurso é um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  

Para fazer a transição dessas cargas de trabalho, vá para a página de propriedades de cogerenciamento e mova o controle deslizante de carga de trabalho do Configuration Manager para **Piloto** ou **Todos**. 

Para saber mais, confira [Cogerenciamento para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Suporte para várias hierarquias para um locatário do Intune
<!--1357944--> Alguns clientes têm várias hierarquias do Configuration Manager e querem consolidá-las no futuro para um único locatário do Azure Active Directory e do Microsoft Intune. O cogerenciamento agora dá suporte a conectar mais de um ambiente do Configuration Manager ao mesmo locatário do Intune.

Para obter mais informações, veja [Preparar dispositivos Windows 10 para cogerenciamento](/sccm/core/clients/manage/co-management-prepare).
 


## <a name="compliance-settings"></a>Configurações de conformidade

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Definir as configurações do Windows Defender SmartScreen para o Microsoft Edge
<!--1353701--> A política de configurações de conformidade de navegador Microsoft Edge adiciona as três configurações a seguir ao Windows Defender SmartScreen: 
- Permitir SmartScreen
- Os usuários podem substituir o aviso do SmartScreen para sites
- Os usuários podem substituir o aviso do SmartScreen para arquivos

Para obter mais informações, veja [Definir configurações do Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


### <a name="scap-extensions"></a>Extensões SCAP
<!--1357552--> Converta o conteúdo do SCAP (Protocolo de Automação de Conteúdo de Segurança) para linhas de base de configurações de conformidade e gere relatórios do SCAP usando uma extensão de console. Esse recurso inclui também um novo painel para visualizar a conformidade do cliente, bem como a conformidade com a regra do XCCDF. 

Para obter mais informações, veja [Sobre extensões do SCAP](/sccm/compliance/plan-design/scap/about-scap).



## <a name="application-management"></a>Gerenciamento de aplicativos

### <a name="phased-deployment-of-applications"></a>Implantação em fases de aplicativos
<!--1358147--> Crie uma implantação em fases para um aplicativo. As implantações em fases permitem que você coordene uma distribuição coordenada e sequenciada do software com base em grupos e critérios personalizáveis. Por exemplo, implante o aplicativo em uma coleção piloto e, em seguida, continue automaticamente a distribuição com base nos critérios de sucesso. 

Para obter mais informações, consulte os seguintes artigos:  

- [Criar uma implantação em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerenciar e monitorar as implantações em fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Provisionar pacotes de aplicativos do Windows para todos os usuários em um dispositivo
<!--1358310--> Provisione um aplicativo com um pacote do aplicativo do Windows para todos os usuários no dispositivo. Um exemplo comum desse cenário é o provisionamento de um aplicativo da Microsoft Store para Empresas e Educação, como o Minecraft: Education Edition, para todos os dispositivos usados pelos alunos em uma escola. Anteriormente, o Configuration Manager somente permitia a instalação desses aplicativos por usuário. Depois de entrar em um novo dispositivo, o aluno precisava esperar para acessar um aplicativo. Agora, quando o aplicativo é provisionado no dispositivo para todos os usuários, eles podem começar a produzir mais rapidamente. 

Para obter mais informações, confira [Criar aplicativos Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração da Ferramenta de Personalização do Office com o Instalador do Office 365
<!--1358149--> A Ferramenta de Personalização do Office agora está integrada ao instalador do Office 365 no console do Configuration Manager. Ao criar uma implantação para o Office 365, defina dinamicamente as configurações de capacidade de gerenciamento mais recentes do Office. A Microsoft atualizará a Ferramenta de Personalização do Office ao lançar novos builds do Office 365. Essa integração permitirá que você aproveite novas configurações de capacidade de gerenciamento no Office 365 assim que elas estiverem disponíveis. 

Para obter mais informações, confira [Implantar aplicativos do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Suporte para novos formatos do pacote do aplicativo do Windows
<!--1357427--> O Configuration Manager agora dá suporte à implantação do novo pacote de aplicativo do Windows 10 (.msix) e formatos do pacote de aplicativo (.msixbundle). 

Para obter mais informações, confira [Criar aplicativos Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_general).


### <a name="uninstall-application-on-approval-revocation"></a>Desinstalar o aplicativo na revogação da aprovação
<!--1357891--> O comportamento mudou para a revogação da aprovação de um aplicativo. Agora, quando você nega a solicitação para o aplicativo, o cliente desinstala o aplicativo do dispositivo do usuário. Esse comportamento exige que você habilite o [recurso opcional](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Aprovar solicitações de aplicativos para usuários por dispositivo**. 

Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications#bkmk_approval) (Implantar aplicativos).


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861--> O Gerenciador de Conversão de Pacote agora é uma ferramenta integrada que permite converter pacotes herdados do Configuration Manager 2007 para os aplicativos do branch atual do Configuration Manager. Em seguida, você pode usar recursos de aplicativos como dependências, regras de requisitos e afinidade de dispositivo de usuário.

Comece com as seguintes ações do nó **Pacotes** no console do Configuration Manager:  

   - **Analisar Pacote**: inicie o processo de conversão analisando o pacote.  

   - **Converter Pacote**: alguns pacotes podem ser convertidos facilmente em aplicativos com essa ação.  

   - **Corrigir e Converter**: alguns pacotes requerem que os problemas sejam corrigidos antes da conversão em aplicativos.  

Em seguida, vá para o painel **Status de Conversão de Pacote** no espaço de trabalho **Monitoramento**. Esse novo painel mostra o estado geral de análise e conversão de pacotes no site. Esse recurso é um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features).



## <a name="os-deployment"></a>Implantação de sistema operacional

### <a name="improvements-to-phased-deployments"></a>Melhorias a implantações em fases

Esta versão inclui as seguintes melhorias às implantações em fases:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Criar uma implantação em fases com fases configuradas manualmente
<!--1358148--> Para uma sequência de tarefas, agora configure manualmente as fases ao criar uma implantação em fases. Adicione até 10 fases extras usando a guia **Fases** do assistente para Criar Implantação em Fases. Você ainda pode criar automaticamente uma implantação padrão em duas fases. 

Para obter mais informações, veja [Criar uma implantação em fases com fases configuradas manualmente](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual).

#### <a name="phased-deployment-status"></a>Status da implantação em fases
<!--1358577--> As implantações em fases agora têm uma experiência de monitoramento nativa. No nó **Implantações** no espaço de trabalho **Monitoramento**, selecione uma implantação em fases e clique em **Status da Implantação em Fases** na faixa de opções. 

Para obter mais informações, veja [Gerenciar e monitorar implantações em fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Distribuição gradual durante as implantações em fases
<!--1358578--> Durante uma implantação em fases, a distribuição em cada fase agora pode acontecer gradualmente. Esse comportamento ajuda a reduzir o risco de problemas de implantação e diminui a carga na rede causada pela distribuição de conteúdo aos clientes. O site pode tornar gradualmente o software disponível, dependendo da configuração de cada fase. Todos os clientes em uma fase têm um prazo em relação à hora em que o software é disponibilizado. A janela entre o horário disponível e o prazo final é a mesma para todos os clientes em uma fase. 

Para obter mais informações, confira [Configurações de fase](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade in-loco do Windows 10
<!--1358500--> O modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 agora inclui outro novo grupo com ações recomendadas para adicionar caso o processo de atualização falhe. Essas ações facilitam a solução de problemas. Uma dessas ferramentas é o Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico autônoma para obter detalhes sobre por que uma atualização do Windows 10 não foi bem-sucedida. 

Para obter mais informações, veja [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias em pontos de distribuição habilitados para PXE
<!--1357580--> Na guia **PXE** das propriedades do ponto de distribuição, verifique **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**. Essa nova opção habilita um respondente PXE no ponto de distribuição, que não requer o WDS (Serviços de Implantação do Windows). Como o WDS não é necessário, o ponto de distribuição habilitado para PXE pode ser um sistema operacional cliente ou servidor, incluindo o Windows Server Core. Esse novo serviço de respondente PXE é compatível com IPv6 e também aumenta a flexibilidade dos pontos de distribuição habilitados para PXE em escritórios remotos. 

Para obter mais informações, veja [Habilitar o PXE no ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Não é necessária conta de acesso à rede para alguns cenários
<!--1358278,1358279--> O recurso [Sistema de sites HTTP aprimorado](#bkmk_ehttp) também remove algumas dependências na conta de acesso de rede. Quando você habilita a nova opção do site para **Usar certificados gerados pelo Configuration Manager para os sistemas de sites HTTP**, os cenários a seguir não exigem uma conta de acesso à rede para baixar conteúdo de um ponto de distribuição:  

- Sequências de tarefas em execução da mídia de inicialização ou do PXE
- Sequências de tarefas em execução no Centro de Software  

Essas sequências de tarefas podem ser usadas para implantação de sistema operacional ou personalização. Também é compatível com computadores de grupo de trabalho.


### <a name="other-improvements-to-os-deployment"></a>Outras melhorias à implantação do sistema operacional

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Mascarar dados confidenciais armazenados nas variáveis da sequência de tarefas
<!--1358330--> Na etapa [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable), selecione a nova opção **Não exibir esse valor**. Por exemplo, ao especificar uma senha. 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Mascarar o nome do programa durante a Etapa de Execução de Comando de uma sequência de tarefas
<!--1358493--> Para impedir que os dados potencialmente confidenciais sejam exibidos ou registrados, defina a variável de sequência de tarefas **OSDDoNotLogCommand** como `TRUE`. Essa variável oculta o nome do programa no smsts.log durante uma etapa da sequência de tarefas [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine).   

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variável de sequência de tarefas para os parâmetros do DISM ao instalar drivers
<!--516679--> Para especificar parâmetros de linha de comando adicionais para o DISM, use a nova variável de sequência de tarefas **OSDInstallDriversAdditionalOptions**. Habilite a configuração da etapa [Aplicar Pacote de Driver](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) para **Instalar o pacote de driver executando DISM com a opção recursiva**. 

#### <a name="option-to-use-full-disk-encryption"></a>Opção para usar a criptografia de disco cheio
<!--SCCMDocs-pr issue 2671--> As etapas [Habilitar BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker) e [Pré-provisionar BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker) agora incluem uma opção para **Usar criptografia de disco completo**. Por padrão, essas etapas criptografam o espaço usado na unidade. Esse comportamento padrão é recomendável, pois é mais rápido e eficiente. Se a sua organização exigir a criptografia de toda a unidade durante a instalação, habilite esta opção. A Instalação do Windows aguarda toda a unidade estar criptografada, o que leva muito tempo, especialmente em unidades grandes. 



## <a name="software-center"></a>Centro de software

### <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura do Centro de Software
<!--1358309--> Funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis ao usuário no Centro de Software. Essa alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. O Centro de Software agora depende do ponto de gerenciamento para obter essas informações, o que ajuda ambientes maiores a serem melhor dimensionados por meio de suas atribuições a [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

> [!Note]  
> As funções de ponto de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessária* na versão 1806, mas ainda são funções *compatíveis*. 
> 
> Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especificar a visibilidade do link do site do catálogo de aplicativos no Centro de Software
<!--1358214--> Use as configurações do cliente para controlar se o link para **Abrir o site do Catálogo de Aplicativos** aparece no nó **Status da instalação** do Centro de Software.  

Para obter mais informações, veja [Configurações de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center).

> [!Note]  
> Não há mais suporte para a **experiência do usuário do Silverlight** para o ponto do site do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Guia personalizada para página da Web no Centro de Software
<!--1358132--> Use as configurações de cliente para criar uma guia personalizada para abrir uma página da Web no Centro de Software. Esse recurso permite que você mostre conteúdo aos usuários finais de forma consistente e confiável. A lista a seguir inclui alguns exemplos:  

- Entrar em contato com TI: informações sobre como entrar em contato com o departamento de TI da sua organização  

- Centro de Suporte de TI: ações de autoatendimento de TI como a pesquisa em uma base de dados de conhecimento ou a abertura de um tíquete de suporte.  

- Documentação do usuário final: artigos para usuários em sua organização em vários tópicos de TI, por exemplo, usar aplicativos ou atualizar para o Windows 10.  

Para obter mais informações, veja [Configurações de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center) e o [Guia do usuário do Centro de Software](/sccm/core/understand/software-center).


### <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131--> O Centro de Software agora exibe a próxima janela de manutenção agendada. Na guia Status da Instalação, alterne a exibição de Todas os para Futuras. Isso exibe o intervalo de tempo e a lista de implantações que estão agendadas. Se não houver mais janelas de manutenção futuras, a lista estará em branco. 

Para obter mais informações, veja [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows) e o [Guia do usuário do Centro de Software](/sccm/core/understand/software-center).



## <a name="software-updates"></a>Atualizações de software

### <a name="third-party-software-updates"></a>Atualizações de software de terceiros
<!--1357605, 1352101, 1358714--> Atualizações de software de terceiros permitem que você assine catálogos de parceiros no console do Configuration Manager e publique as atualizações no WSUS. Em seguida, você pode implantar essas atualizações usando o processo de gerenciamento de atualizações de software existente. 

Para obter mais informações, veja [Habilitar atualizações de terceiros](/sccm/sum/deploy-use/third-party-software-updates).


### <a name="deploy-software-updates-without-content"></a>Implantar atualizações de software sem conteúdo
<!--1357933--> Implante atualizações de software a dispositivos sem precisar primeiro baixar e distribuir o conteúdo da atualização de software para os pontos de distribuição. Esse recurso será útil para lidar com um conteúdo de atualização muito grande ou quando você quiser que os clientes sempre obtenham o conteúdo por meio do serviço de nuvem do Microsoft Update. Os clientes nesse cenário também podem baixar o conteúdo de pares que já tenham o conteúdo necessário. O cliente do Configuration Manager continua a gerenciar o download de conteúdo, portanto, é possível usar o recurso de cache par do Configuration Manager ou outras tecnologias, como a Otimização de Entrega. Esse recurso permite qualquer tipo de atualização compatível com o gerenciamento de atualizações de software do Configuration Manager, incluindo as atualizações do Windows e do Office. 

Para obter mais informações, veja a opção **Nenhum pacote de implantação** quando você [Implantar manualmente atualizações de software](/sccm/sum/deploy-use/manually-deploy-software-updates) ou [Implantar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implantação automática pela arquitetura de atualização de software
 <!--1322266--> Agora você pode filtrar ADRs (regras de implantação automática) para excluir arquiteturas como Itanium e ARM64. Na página **Atualizações de Software** do Assistente para Criar Regra de Implantação Automática, o filtro de propriedade **Arquitetura** agora está disponível. 

Para mais informações, confira [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates) (Implantar atualizações de software automaticamente).


### <a name="improved-wsus-maintenance"></a>Manutenção aprimorada do WSUS 
<!--1357898--> O Assistente de limpeza do WSUS agora recusa atualizações que expiraram conforme as regras de substituição definidas nas propriedades de componente de ponto de atualização de software. 

Para obter mais informações, veja [Manutenção de atualizações de software](/sccm/sum/deploy-use/software-updates-maintenance).



## <a name="reporting"></a>Relatórios

### <a name="new-software-updates-compliance-report"></a>Novo relatório de conformidade de atualizações de software
<!--1357775--> A exibição da conformidade de relatórios de atualizações de software tradicionalmente inclui dados de clientes que não entraram em contato com o site recentemente. Um novo relatório, **Conformidade 9 – integridade e conformidade gerais**, permite filtrar os resultados de conformidade para um grupo de atualização de software específico por clientes "íntegros". Este relatório mostra o estado de conformidade mais realista de clientes ativos em seu ambiente. 

Para obter mais informações, veja [Relatórios de atualizações de software](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports).



## <a name="inventory"></a>Inventário

### <a name="bkmk_bigint"></a> Melhoria ao inventário de hardware para grandes valores inteiros
<!--1357880--> O inventário de hardware antes tinha um limite para inteiros maiores que 4.294.967.296 (2^32). Esse limite podia ser alcançado para atributos como tamanhos de disco rígido em bytes. O ponto de gerenciamento não processava valores inteiros acima desse limite, portanto, nenhum valor era armazenado no banco de dados. Agora, nesta versão, o limite é aumentado para 18,446,744,073,709,551,616 (2^64). 

Para obter mais informações, veja [Uso de valores inteiros grandes](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Revisão da unidade padrão do inventário de hardware
<!--514442--> No [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), a unidade padrão usada em vários modos de exibição de relatórios foi alterada de MB (megabytes) para GB (gigabytes). Devido às [Melhoria no inventário de hardware para grandes valores inteiros](#bkmk_bigint) e com base nos comentários dos clientes, essa unidade padrão voltou a ser MB.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Console do Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Painel do Ciclo de Vida do Produto
<!--1319632--> O painel de ciclo de vida do produto mostra o estado da Política do Ciclo de Vida da Microsoft para produtos da Microsoft instalados em dispositivos gerenciados com o Configuration Manager. Ele também fornece informações sobre os produtos da Microsoft em seu ambiente, o estado da capacidade de suporte e as datas de término do suporte. Use o painel para entender a disponibilidade do suporte para cada produto. Essas informações ajudam a planejar quando atualizar os produtos da Microsoft que você usa antes que eles atinjam o término do suporte atual.   

Para obter mais informações, veja [Painel de ciclo de vida do produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="copy-asset-details-from-monitoring-views"></a>Copiar detalhes do ativo das exibições de monitoramento
<!--1357856--> As seguintes áreas do espaço de trabalho **Monitoramento** agora são compatíveis com cópia de texto:  

- No nó **Implantações**, selecione uma implantação e clique em **Exibir Status**. No painel **Detalhes do Ativo** da exibição de Status de Implantação, selecione um ou mais dispositivos.  

- Expanda o nó **Status de Distribuição** e selecione **Status do Conteúdo**. Selecione um software e clique em **Status da Exibição**. No painel **Detalhes do Ativo** da exibição de Status do Conteúdo, selecione um ou mais pontos de distribuição. 

Clique com o botão direito do mouse no ativo e selecione **Copiar**. Essa ação copia os ativos selecionados como uma lista delimitada por vírgulas que inclui os detalhes completos. O atalho de teclado **CTRL** + **C** também funciona nesses modos de exibição. 

Para obter mais informações, veja [Melhorias do console na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="improvements-to-the-surface-dashboard"></a>Melhorias no painel do Surface
<!--1358654--> Esta versão inclui as seguintes melhorias ao painel do Surface:  

- O painel do Surface agora exibe uma lista de dispositivos relevantes quando você seleciona seções específicas do grafo:  

   - Clicar no bloco **Percentual de dispositivos do Surface** abre uma lista de dispositivos do Surface.  

   - Clicar em uma barra no bloco **Cinco Principais Versões de Firmware** abre uma lista de dispositivos do Surface com essa versão de firmware específica.  

- Ao exibir essas listas de dispositivo no painel do Surface, clique com o botão direito do mouse em um dispositivo para executar ações comuns.  

Para obter mais informações, veja o [painel do Surface](/sccm/core/clients/manage/surface-device-dashboard).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Exibir o usuário conectado no momento para um dispositivo
<!--1358202--> Agora, por padrão, o nó **Dispositivos** do espaço de trabalho **Ativos e Conformidade** exibe uma coluna para o **Usuário Conectado no Momento**. Ele também é exibido para qualquer lista de dispositivos específicos da coleção. Este valor é tão atual quanto o [status do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). Quando o usuário faz logoff, o cliente limpa esse valor. Se nenhum usuário estiver conectado, o valor ficará em branco. 

Para obter mais informações, veja [Melhorias do console na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Enviar comentários do console do Configuration Manager  
<!--1357542-->

Mande um sorriso! Agora, você pode informar diretamente a equipe do Configuration Manager sobre suas experiências. Enviar comentários do console do Configuration Manager é muito fácil. Queremos ouvir todos os seus comentários: elogios, problemas e sugestões. No console do Configuration Manager, clique no botão de sorriso no canto superior direito, acima da faixa de opções. Esse comentário vai diretamente para a equipe de produtos da Microsoft do Configuration Manager. Apesar de o Hub de Comentários do Windows 10 ainda ter suporte, incentivamos o uso do mecanismo de comentários no console.  

Para obter mais informações, veja [Melhorias ao console na versão 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) e [Comentários sobre o produto](/sccm/core/understand/find-help#BKMK_1806Feedback).



## <a name="next-steps"></a>Próximas etapas

Quando estiver pronto para instalar esta versão, veja [Instalação de atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).

> [!TIP]  
> Para instalar um novo site, use uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalação de novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Para problemas conhecidos e significativos, veja [Notas de versão](/sccm/core/servers/deploy/install/release-notes).