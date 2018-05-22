---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis no Technical Preview do Configuration Manager versão 1805.
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb2b25440c87d4969d152ce410b8a28f010868ce
ms.sourcegitcommit: 021272d5858e5dbb650b95644736d1de3dab7d8a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2018
---
# <a name="capabilities-in-technical-preview-1805-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1805 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do Configuration Manager, versão 1805. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Technical Preview. 

Examine o artigo de [Technical Preview](/sccm/core/get-started/technical-preview) antes de instalar essa atualização. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Criar uma implantação em fases com fases configuradas manualmente para uma sequência de tarefas
<!--1358148--> 
Agora você pode [criar uma implantação em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) com fases configuradas manualmente para uma sequência de tarefas. Você pode adicionar até 10 fases adicionais na guia **Fases** do assistente Criar Implantação em Fases. 


### <a name="try-it-out"></a>Experimente!
Siga as instruções para criar uma implantação em fases, em que você configura manualmente todas as fases. Envie seus [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou. 

1. No espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Clique com o botão direito do mouse em uma sequência de tarefas existente e selecione **Criar Implantação em Fases**.  

3. Na guia **Geral**, forneça um nome, uma descrição (opcional) à implantação em fases e selecione **Configurar manualmente todas as fases**.  

4. Na guia **Fases**, clique em **Adicionar**.  

5. Especifique um **Nome** para a fase e navegue para a **Coleção de Fases** de destino.  

6. Na guia **Configurações de Fase**, escolha uma opção para cada uma das configurações de agendamento e selecione **Avançar** quando concluir.  

    - Critérios para o sucesso da fase anterior (esta opção está desabilitada para a primeira fase).
        - **Percentual de sucesso da implantação**: especifique o percentual de dispositivos que concluíram com êxito a implantação de acordo com os critérios de sucesso da fase anterior.  

    - Condições para começar esta fase de implantação após êxito da fase anterior  
        - **Iniciar automaticamente esta fase após um período de adiamento (em dias)**: escolha o número de dias de espera antes do início da fase seguinte após o sucesso da fase anterior. 
        - **Iniciar manualmente esta fase da implantação**: não inicie esta fase automaticamente após o sucesso da fase anterior.  

    - Uma vez que um dispositivo for definido como destino, instale o software
        - **Assim que possível**: define a data limite da instalação no dispositivo assim que o dispositivo é direcionado.
        - **Hora limite (em relação à hora em que o dispositivo é direcionado)**: define a data limite da instalação com determinado número de dias depois que o dispositivo é direcionado.  
     
7. Conclua o assistente Configurações de Fase.

8. Na guia **Fases** do assistente Criar Implantação em Fases, agora você pode adicionar, remover, reorganizar ou editar as fases dessa implantação.  

9. Conclua o Assistente para Criar Implantação em Fases.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Suporte a ponto de distribuição na nuvem para o Azure Resource Manager
<!--1322209-->
Ao criar uma instância do [ponto de distribuição na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure), o assistente agora oferece a opção de criar uma **implantação do Azure Resource Manager**. O [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implantar o ponto de distribuição na nuvem com o Azure Resource Manager, o site usa o Azure Active Directory (Azure AD) para autenticar e criar os recursos necessários para a nuvem. Esta implantação modernizada não requer o certificado de gerenciamento do Azure clássico.  

O assistente do ponto de distribuição na nuvem ainda fornece a opção para uma **implantação de serviço clássico** usando um certificado de gerenciamento do Azure. Para simplificar a implantação e o gerenciamento de recursos, recomendamos usar o modelo de implantação do Azure Resource Manager para todos os pontos de distribuição na nuvem. Se possível, reimplante os pontos de distribuição na nuvem existentes por meio do Gerenciador de Recursos.

O Configuration Manager não migra os pontos de distribuição na nuvem clássicos existentes para o modelo de implantação do Azure Resource Manager. Crie novos pontos de distribuição de nuvem usando implantações do Azure Resource Manager e remova os pontos de distribuição de nuvem clássicos. 

> [!IMPORTANT]  
> Esse recurso não habilita o suporte para o Provedor de Serviços de Nuvem (CSP) do Azure. A implantação do ponto de distribuição na nuvem com o Azure Resource Manager continua a usar o serviço de nuvem clássico, ao qual o CSP não oferece suporte. Para saber mais, confira os [serviços do Azure disponíveis no CSP do Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Pré-requisitos  
- Integração com o [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). A descoberta do usuário do Azure AD não é necessária.  

- Os mesmos [requisitos para o ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_PrereqsCloudDP), com exceção do certificado de gerenciamento do Azure.  


### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, no espaço de trabalho **Administração**, expanda **Serviços de Nuvem** e selecione **Pontos de Distribuição de Nuvem**. Clique em **Criar Ponto de Distribuição de Nuvem** na faixa de opções.   

2. Na página **Geral**, selecione **implantação do Azure Resource Manager** . Clique em **Entrar** para autenticar com uma conta de administrador de assinatura do Azure. O assistente automatiza os campos restantes das informações de assinatura do Azure AD armazenadas durante o pré-requisito de integração. Se você possui várias assinaturas, selecione a assinatura desejada para usar. Clique em **Avançar**.  

3. Na página **Configurações**, forneça o **arquivo de certificado** do servidor PKI como de costume. Este certificado define o **FQDN do Serviço** do ponto de distribuição de nuvem usado pelo Azure. Selecione a **Região** e, em seguida, selecione uma opção de grupo de recursos para **Criar novo** ou **Usar o existente**. Insira o novo nome do grupo de recursos ou selecione um grupo de recursos existente na lista suspensa.  

4. Conclua o assistente.  

> [!NOTE]  
> Para o aplicativo de servidor do AD Azure selecionado, o Azure atribui a permissão **colaborador** de assinatura.  

Monitore o progresso da implantação do serviço com o **cloudmgr.log** no ponto de conexão do serviço.



## <a name="take-actions-based-on-management-insights"></a>Realizar ações com base em insights de gerenciamento
<!--1357930-->
Alguns [insights de gerenciamento](/sccm/core/servers/manage/management-insights) agora têm a opção de executar uma ação. Dependendo da regra, essa ação exibe um dos seguintes comportamentos:  

- Navegar automaticamente no console até o nó, onde você pode realizar outras ações. Por exemplo, se a percepção do gerenciamento recomenda alterar uma configuração de cliente, a ação leva para o nó Configurações do Cliente. Você pode tomar outras medidas modificando o objeto padrão ou personalizado de configurações do cliente.  

- Navegar para uma visualização filtrada com base em uma consulta. Por exemplo, a ação na regra de coleções vazias mostra apenas essas coleções na lista de coleções. Aqui você pode tomar outras medidas, como excluir uma coleção ou modificar suas regras de participação.  

As seguintes regras de insight de gerenciamento possuem ações nesta liberação:
- Segurança
    - Versões do cliente de antimalware sem suporte
- Centro de software
    - Usar a nova versão do Centro de Software
- Aplicativos
    - Aplicativos sem implantações
- Gerenciamento simplificado
    - Versões de Cliente Não CB
- Coleções
    - Coleções vazias 
- Cloud Services
    - Atualizar clientes para a versão mais recente do Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Transição da carga de trabalho do dispositivo para o Intune usando o cogerenciamento
<!--1357903-->

Você pode agora transitar a carga de trabalho da configuração do dispositivo a partir do Configuration Manager para o Intune depois de ativar o cogerenciamento. A transição dessa carga de trabalho permite usar o Intune para implantar políticas do MDM e, ao mesmo tempo, continuar usando o Configuration Manager para implantar aplicativos. 

Para transferir a carga de trabalho, acesse a página de propriedades de cogerenciamento e mova a barra deslizante do Configuration Manager para **Piloto** ou **Todos**. Para saber mais, confira [Cogerenciamento para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).

> [!Note]  
> Mover essa carga de trabalho também move as cargas de trabalho **Acesso de Recurso** e **Endpoint Protection**, que são um subconjunto da carga de trabalho de configuração do dispositivo.

Quando você faz a transição dessa carga de trabalho, ainda é possível implantar configurações do Configuration Manager para dispositivos cogerenciados, mesmo que o Intune seja a autoridade de configuração do dispositivo. Essa exceção pode ser usada para definir configurações exigidas pela sua organização, mas ainda não disponíveis no Intune. Especifique essa exceção em uma linha de base de configuração do Configuration Manager. Ative a opção para **Sempre aplicar essa linha de base, mesmo para clientes cogerenciados**  ao criar a linha de base, ou na guia **Geral** das propriedades de uma linha de base existente. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Habilitar pontos de distribuição para usar o controle de congestionamento de rede
<!--1358112-->

O Windows Low Extra Delay Background Transport (LEDBAT) é um recurso do Windows Server para ajudar a gerenciar as transferências de rede em segundo plano. Para pontos de distribuição em execução nas versões com suporte do Windows Server, você pode ativar uma opção para ajudar a ajustar o tráfego da rede. Os clientes usam a largura de banda da rede somente quando ela está disponível. 

Para saber mais sobre o Windows LEDBAT, confira a postagem no blog [Novos avanços de transporte](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/).


### <a name="prerequisites"></a>Pré-requisitos
- Um ponto de distribuição no Windows Server, versão 1709.  

- Um dispositivo cliente executando pelo menos o Windows 10, versão 1607.


### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Selecione o nó **Pontos de Distribuição**. Selecione o ponto de distribuição de destino e clique em **Propriedades** na faixa de opções.  

2. Na guia **Geral**, habilite a opção para **Ajustar a velocidade de download para usar a largura de banda de rede não utilizada (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Painel de gerenciamento de nuvem
<!--1358461-->
O novo **painel de gerenciamento de nuvem** fornece uma visão centralizada do uso do gateway de gerenciamento de nuvem (CMG). Quando o site é integrado ao Azure AD, ele também exibe dados sobre usuários e dispositivos da nuvem.  

A captura de tela a seguir é uma parte do painel de gerenciamento de nuvem que mostra dois dos blocos disponíveis:  
![O painel de controle do gerenciamento de nuvem faz o rastreamento do tráfego CMG e dos clientes online atuais](media/1358461-cmg-dashboard.png)

Esse recurso também inclui o **Analisador de conexão CMG** para verificação em tempo real para auxiliar na solução de problemas. O utilitário no console verifica o status atual do serviço e o canal de comunicação por meio da conexão CMG aponta para os pontos de gerenciamento que permitem o tráfego CMG.


### <a name="prerequisites"></a>Pré-requisitos
- Um [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) ativo usado por clientes baseados na Internet.  

- O site foi integrado aos [serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para gerenciamento de nuvem.  


### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

#### <a name="cloud-management-dashboard"></a>Painel de gerenciamento de nuvem

No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**. Selecione o nó **Gerenciamento de Nuvem** e visualize os blocos do painel.  

#### <a name="cmg-connection-analyzer"></a>Analisador de conexão de CMG

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Serviços de Nuvem** e selecione **Gateway de Gerenciamento de Nuvem**.  

2. Selecione a instância CMG de destino e, em seguida, selecione **Analisador de Conexões** na faixa de opções.  

3. Na janela do analisador de conexões CMG, selecione uma das seguintes opções para autenticar com o serviço:  

     1. **Usuário do Azure AD**: use essa opção para simular a comunicação da mesma forma que uma identidade de usuário baseada na nuvem conectada a um dispositivo Windows 10 associado ao Azure AD. Clique em **Entrar** para inserir com segurança as credenciais dessa conta de usuário do Azure AD.  

     2. **Certificado de cliente**: use essa opção para simular a comunicação da mesma forma que um cliente do Configuration Manager com um [certificado de autenticação de cliente ](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Clique em **Iniciar** para iniciar a análise. Os resultados são exibidos na janela do analisador. Selecione uma entrada para ver mais detalhes no campo Descrição.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
O Configuration Manager sempre forneceu um grande armazenamento centralizado de dados do dispositivo, que os clientes usam para fins de relatório. No entanto, esses dados são úteis somente no momento em que foram coletados dos clientes. 

O CMPivot é um novo utilitário no console que fornece acesso ao estado dos dispositivos em tempo real em seu ambiente. Ele executa imediatamente uma consulta em todos os dispositivos atualmente conectados na coleção de destino e retorna os resultados. Você pode então filtrar e agrupar esses dados na ferramenta. Ao fornecer dados em tempo real de clientes online, você pode responder a perguntas de negócios com mais rapidez, solucionar problemas e responder a incidentes de segurança.

Por exemplo, na [mitigação das vulnerabilidades do canal de execução especulativa](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), um dos requisitos é atualizar o BIOS do sistema. Você pode usar o CMPivot para consultar rapidamente as informações do BIOS do sistema e localizar clientes que não estejam em conformidade. 

Nesta captura de tela, o CMPivot exibe duas versões separadas do BIOS com uma contagem de dispositivos de cada um. Você pode usar esta consulta de exemplo ao experimentar o CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![A janela CMPivot com consulta de exemplo para BIOSVersion](media/1358456-cmpivot-biosversion.png)

Você pode clicar na contagem de dispositivos para detalhar os dispositivos específicos. Ao exibir dispositivos no CMPivot, você pode clicar com o botão direito do mouse em um dispositivo e selecionar as seguintes [ações de notificação do cliente](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode):
- Executar Script
- Controle remoto
- Gerenciador de Recursos

Ao clicar com o botão direito do mouse em um dispositivo específico, você também pode dinamizar a visualização do dispositivo específico para um dos seguintes atributos:
- Comandos de inicialização automática
- Produtos instalados
- Processos
- Serviços
- Usuários
- Conexões ativas
- Atualizações ausentes

### <a name="prerequisites"></a>Pré-requisitos
- Os clientes de destino devem ser atualizados para a versão mais recente.  

- O administrador do Configuration Manager precisa de permissões para executar scripts. Para saber mais, veja [Funções de segurança para scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Ativos e Conformidade** e selecione **Coleções de Dispositivos**. Selecione uma coleção de destino e clique em **Iniciar CMPivot** na faixa de opções para iniciar a ferramenta.  

2. A interface fornece mais informações sobre o uso da ferramenta. 
     - Você pode inserir manualmente as cadeias de caracteres de consulta na parte superior ou clicar nos links na documentação em linha.
     - Clique em uma das **Entidades** para adicioná-la à cadeia de caracteres de consulta. 
     - Os links para **Operadores de Tabela**, **Funções de Agregação** e **Funções Escalares** abrem a documentação de referência da linguagem no navegador da Web. O CMPivot usa a mesma linguagem de consulta do [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).



## <a name="improved-secure-client-communications"></a>Comunicações aprimoradas de cliente seguro
<!--1356889,1358228,1358460-->
O uso da comunicação HTTPS é recomendado para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução da integração do Azure AD (Azure Active Directory) reduz alguns, mas não todos os requisitos de certificado. 

Esta versão inclui melhorias em como os clientes se comunicam com os sistemas de sites. Há dois objetivos principais para essas melhorias:  

- Você pode proteger a comunicação do cliente sem a necessidade de certificados de autenticação do servidor PKI.  

- Os clientes podem acessar com segurança o conteúdo dos pontos de distribuição sem a necessidade de uma conta de acesso à rede.  

> [!Note]  
> Os certificados PKI ainda são uma opção válida para os clientes que desejam usá-los.  


### <a name="bkmk_token"></a> Cenários
Os cenários a seguir se beneficiam dessas melhorias:  

#### <a name="bkmk_token1"></a> Cenário 1: Cliente para o ponto de gerenciamento
<!--1356889-->
[Os dispositivos associados ao Azure AD](/azure/active-directory/device-management-introduction#azure-ad-joined-devices) podem se comunicar por meio de um gateway de gerenciamento de nuvem (CMG) com um ponto de gerenciamento configurado para HTTP. O servidor do site gera um certificado para o ponto de gerenciamento, permitindo que ele se comunique por meio de um canal seguro.   

> [!Note]  
> Esse comportamento foi alterado na versão 1802 do branch atual do Configuration Manager, que requer um ponto de gerenciamento habilitado para HTTPS para esse cenário. Para obter mais informações, consulte [Habilitar ponto de gerenciamento para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

#### <a name="bkmk_token2"></a> Cenário 2: Cliente para o ponto de distribuição
<!--1358228-->
Um cliente associado ao grupo de trabalho ou ao Azure AD pode fazer o download do conteúdo por meio de um canal seguro a partir de um ponto de distribuição configurado para HTTP.   

#### <a name="bkmk_token3"></a> Cenário 3: Identidade de dispositivo do Azure AD 
<!--1358460-->
Um dispositivo do Azure AD associado ou [híbrido do Azure AD](/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) sem um usuário do AD do Azure conectado pode se comunicar com segurança com o site atribuído. A identidade do dispositivo baseado em nuvem agora é suficiente para autenticar com o CMG e o ponto de gerenciamento.  


### <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gerenciamento configurado para conexões de cliente HTTP. Defina essa opção na guia **Geral** das propriedades da função do sistema de sites.  

- Um ponto de distribuição configurado para conexões de cliente HTTP. Defina essa opção na guia **Geral** das propriedades da função do sistema de sites. Não habilite a opção para **Permitir que os clientes se conectem anonimamente**.  

- Um gateway de gerenciamento de nuvem.  

- Integrar o site ao Azure AD para gerenciamento de nuvem.  

    - Se você já atingiu esse pré-requisito para o seu site, precisa atualizar o aplicativo do Azure AD. No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Serviços de Nuvem** e selecione **Locatários do Azure Active Directory**. Selecione o locatário do Azure AD, selecione o aplicativo Web no painel **​​Aplicativos** e clique em **Atualizar Configuração do Aplicativo** na faixa de opções.  

- Um cliente que executa o Windows 10 versão 1803 e ingressou no Azure AD. (Este requisito destina-se tecnicamente apenas ao [Cenário 3](#bkmk_token3).) 


### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Configuração do Site** e selecione **Sites**. Selecione o site e clique em **Propriedades** na faixa de opções.  

2. Alterne para a guia **Comunicação do Computador Cliente**. Selecione a opção para **HTTPS ou HTTP** e, em seguida, ative a nova opção para **Usar certificados gerados pelo Configuration Manager para sistemas de site HTTP**.  

Veja a lista [anterior dos cenários](#bkmk_token) para validar.

> [!Tip]
> Nesta versão, aguarde até 30 minutos para o ponto de gerenciamento receber e configurar o novo certificado do site.

Você pode ver esses certificados no console do Configuration Manager. Acesse o espaço de trabalho **Administração**, expanda **Segurança** e selecione o nó **Certificados**. Procure o certificado raiz **Emissão de SMS**, bem como os certificados de função de servidor do site emitidos pela raiz de emissão do SMS.


### <a name="known-issues"></a>Problemas conhecidos
- O usuário não pode visualizar no Centro de Software nenhum aplicativo destinado a ele, conforme disponível.  

- Os cenários de implantação de SO ainda exigem a conta de acesso à rede.  

- Habilitar e desabilitar rápida e repetidamente a opção para **Usar certificados gerados pelo Configuration Manager para sistemas de site HTTP** pode fazer com que o certificado não seja vinculado adequadamente às funções do sistema de sites. Nenhum certificado emitido pelo certificado "Emissão de SMS" está vinculado a um site no IIS (Serviços de Informações da Internet) do Windows Server. Para contornar esse problema, exclua todos os certificados emitidos por "Emissão de SMS Issuing" do armazenamento de certificados **SMS**  no Windows e reinicie o serviço smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Melhorias para habilitar o suporte de atualização de software de terceiros
<!--1357605-->
Como resultado de seus comentários do UserVoice no [suporte de atualização de software de terceiros](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), essa versão itera ainda mais sobre a integração com o System Center Updates Publisher (SCUP). A visualização técnica [versão 1803](/sccm/core/get-started/capabilities-in-technical-preview-1803#enable-third-party-software-update-support-on-clients) do Configuration Manager adicionou a capacidade de ler o certificado do WSUS para atualizações de terceiros e, em seguida, implantar esse certificado nos clientes. Mas você ainda precisava usar a ferramenta SCUP para criar e gerenciar o certificado para assinar atualizações de software de terceiros.

Nesta versão, você pode habilitar o site do Configuration Manager para configurar automaticamente o certificado. O site comunica-se com o WSUS para gerar um certificado para essa finalidade. O Configuration Manager continua então a implantar esse certificado para os clientes. Essa iteração elimina a necessidade de usar a ferramenta SCUP para criar e gerenciar o certificado. 

Para saber mais sobre o uso geral da ferramenta SCUP, confira [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

### <a name="prerequisites"></a>Pré-requisitos
- Ativar e implantar a configuração do cliente **Habilitar atualizações de software de terceiros** no grupo **Atualizações de Software**.
- Se o WSUS estiver em um servidor separado do ponto de atualização de software, você deverá executar uma das seguintes opções no servidor remoto do WSUS:
    - Habilitar o serviço Registro Remoto no Windows  
    ou
    - Na chave do registro `HKLM\Software\Microsoft\Update Services\Server\Setup`, crie um novo DWORD denominado **EnableSelfSignedCertificates** com um valor de `1`. 

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda a **Configuração do site** e selecione **Sites**. Selecione o site de nível superior, clique em **Configurar Componentes do Site** na faixa de opções e selecione **Ponto de Atualização de Software**.  

2. Mude para a guia **Atualizações de Terceiros**. Selecione a opção **Habilitar atualizações de software de terceiros**, e selecione a opção **Configuration Manager gerencia automaticamente o certificado**.

3. Continue com o restante do fluxo de trabalho típico do SCUP para importar um catálogo de atualizações de software de terceiros e implante as atualizações para os clientes.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade in-loco do Windows 10
<!--1358500-->

O modelo de sequência de tarefas padrão para o upgrade in-loco do Windows 10 agora inclui outro novo grupo com ações recomendadas para adicionar caso o processo de atualização falhe. Essas ações facilitam a solução de problemas.

### <a name="new-groups-under-run-actions-on-failure"></a>Novos grupos em **Executar Ações com Falha**
- **Coletar logs**: para reunir logs do cliente, adicione etapas nesse grupo. 
    - Uma prática comum é copiar os arquivos de log para um compartilhamento de rede. Para estabelecer essa conexão, use a etapa [Conectar à Pasta de Rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder). 
    - Para executar a operação de cópia, use um script ou utilitário personalizado com a etapa [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [Executar script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).
    - Os arquivos a coletar podem incluir os seguintes logs:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Para saber mais sobre o setupact.log e outros logs da Instalação do Windows, confira [Arquivos de Log de Instalação do Windows](/windows/deployment/upgrade/log-files).
    - Para saber mais sobre logs do cliente do Configuration Manager, confira [Logs do cliente do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)
    - Para saber mais sobre _SMSTSLogPath e outras variáveis ​​úteis, confira [Variáveis ​​internas da sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables)

- **Executar as ferramentas de diagnóstico**: para executar ferramentas de diagnóstico adicionais, adicione etapas neste grupo. Essas ferramentas devem ser automatizadas para coletar informações adicionais do sistema logo após a falha.
    - Uma dessas ferramentas é o Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico autônoma que você pode usar para obter detalhes sobre o motivo pelo qual uma atualização do Windows 10 não foi bem-sucedida.
         - No Configuration Manager, [crie um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para a ferramenta.
         - Adicionar uma etapa [Executar Linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) para este grupo da sua sequência de tarefas. Use a opção **Pacote** para fazer referência à ferramenta. A cadeia de caracteres a seguir é um exemplo de **Linha de Comando**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace instalado com o cliente
<!--1357971-->

A ferramenta de visualização de log do CMTrace agora é instalada automaticamente junto com o cliente do Configuration Manager. Ela é adicionada ao diretório de instalação do cliente, que por padrão é `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> O CMTrace *não* é registrado automaticamente no Windows para abrir a extensão de arquivo .log.



## <a name="improvement-to-the-configuration-manager-console"></a>Melhoria no console do Configuration Manager
<!--1358202-->
Fizemos a seguinte melhoria no console do Configuration Manager:

- As listas de dispositivos em Ativos e Conformidade, Dispositivos, agora, por padrão, exibem o usuário conectado no momento. Este valor é tão atual quanto o [status do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). O valor será apagado quando o usuário fizer logoff. Se nenhum usuário estiver conectado, o valor fica em branco. 

### <a name="known-issues"></a>Problemas conhecidos
O valor do usuário atualmente conectado está em branco no nó Dispositivos ou ao exibir uma lista de dispositivos no nó Coleções de Dispositivos. Para contornar esse problema, faça o download deste [Script SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Execute o sp_BgbUpdateLiveData.sql no servidor de banco de dados do site e, em seguida, reinicie os serviços smsexec e sms_notification_server no ponto de gerenciamento.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Melhorias nos comentários do console
<!--1357542-->
Esta versão inclui as seguintes melhorias no novo mecanismo de [Comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) no console do Configuration Manager:  

- A caixa de diálogo de feedback agora lembra suas configurações anteriores, como as opções selecionadas e seu endereço de email.  

- Agora, ele dá suporte a comentários offline. Salve seus comentários no console e faça o upload para a Microsoft em um sistema conectado à Internet. Use a nova ferramenta de envio de comentários offline localizada em `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Para ver as opções de linha de comandos disponíveis e necessárias, execute a ferramenta com a opção `--help`. O sistema conectado precisa de acesso a **petrol.office.microsoft.com**.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias em pontos de distribuição habilitados para PXE
<!--1357580-->

Esta versão inclui as seguintes melhorias adicionais quando você usa a opção para [**Habilitar um respondente PXE sem o Serviço de Implantação do Windows**](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points) em um ponto de distribuição:  

- As regras do Firewall do Windows são criadas automaticamente no ponto de distribuição quando você ativa essa opção  
- Melhorias no log de componentes



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Melhoria no inventário de hardware para grandes valores inteiros
<!--1357880-->
Atualmente, o inventário de hardware tem um limite para números inteiros maiores que 4,294,967,296 (2^32). Esse limite pode ser alcançado para atributos como tamanhos de disco rígido em bytes. O ponto de gerenciamento não processa valores inteiros acima desse limite, portanto, nenhum valor é armazenado no banco de dados. Agora, nesta versão, o limite é aumentado para 18,446,744,073,709,551,616 (2^64). 

Para uma propriedade com um valor que não é alterado, como o tamanho total do disco, talvez não seja possível observar o valor logo após atualizar o site. A maioria dos inventários de hardware é um relatório delta. O cliente envia somente os valores que são alterados. Para contornar esse comportamento, adicione outra propriedade à mesma classe. Essa ação faz com que o cliente atualize todas as propriedades na classe que foi alterada. 



## <a name="improvement-to-wsus-maintenance"></a>Melhoria na manutenção do WSUS
<!--1357898-->

O assistente de limpeza do WSUS agora recusa as atualizações expiradas ou substituídas de acordo com as regras de substituição. Essas regras são definidas nas propriedades do componente de ponto de atualização de software.

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda a **Configuração do site** e selecione **Sites**. Selecione o site de nível superior, clique em **Configurar Componentes do Site** na faixa de opções e selecione **Ponto de Atualização de Software**.  

2. Mude para a guia **Regras de Substituição**. Habilitar a opção para **Execute o assistente de limpeza do WSUS**. Especifique o comportamento de substituição desejado.  

3. Examine o arquivo WSyncMgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Melhoria para o suporte a certificados do CNG
<!--1357314-->
Nesta versão, use [certificados do CNG](/sccm/core/plan-design/network/cng-certificates-overview) para as seguintes funções de servidor habilitadas para HTTPS adicionais:  
- Ponto de registro de certificado, incluindo o servidor NDES com o módulo de política do Configuration Manager



## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
