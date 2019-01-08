---
title: Visualização técnica 1806
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis na visualização técnica 1806 do Configuration Manager.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8914c9ff7a33d24b5d68893018edff8d8e0de444
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424273"
---
# <a name="capabilities-in-technical-preview-1806-for-system-center-configuration-manager"></a>Funcionalidades na visualização técnica 1806 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na visualização técnica do Configuration Manager, versão 1806. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Technical Preview. 

Examine o artigo de [Technical Preview](/sccm/core/get-started/technical-preview) antes de instalar essa atualização. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview

### <a name="ki_contentlib"></a> O site falha ao ser atualizado com a biblioteca de conteúdo remota
<!--514642--> O site falha ao ser atualizado com os seguintes erros em **cmupdate.log**:  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Esse problema ocorre nesta versão quando a biblioteca de conteúdo está em um local remoto.

#### <a name="workaround"></a>Solução alternativa
Mova a biblioteca de conteúdo para uma unidade local do servidor do site. Para obter mais informações, confira [Configurar uma biblioteca de conteúdo remota para o servidor do site](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server). 



</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  



## <a name="bkmk-3pupdate"></a> Atualizações de software de terceiros
<!--1352101--> Essa versão aumenta ainda mais o suporte para atualizações de software de terceiros, como resultado de seus [comentários no UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Não é mais necessário usar o SCUP (System Center Updates Publisher) em alguns cenários comuns. O novo nó **Catálogos de Atualização de Software de Terceiros** no console do Configuration Manager permite que você assine catálogos de terceiros, publique suas atualizações em seu ponto de atualização de software e, em seguida, implante-as nos clientes. 

Os seguintes catálogos de atualização de software de terceiros estão disponíveis nesta versão:

 | Publisher | Nome do Catálogo |
 |--------|---------------------|
 | HP | Catálogo de atualizações de cliente da HP |

O SCUP continua compatível com outros cenários e catálogos. A lista de catálogos no nó Catálogos de Atualização de Software de Terceiros do console do Configuration Manager é dinâmica e será atualizada à medida que mais catálogos forem disponibilizados e receberem suporte.


### <a name="prerequisites"></a>Pré-requisitos
- Configure o gerenciamento de atualizações de software com um ponto de atualização de software habilitado para HTTPS. Para obter mais informações, consulte [Preparar-se para o gerenciamento de atualização de software](/sccm/sum/get-started/prepare-for-software-updates-management).  
  - O ponto de atualização de software precisa estar no servidor do site para esse recurso nesta versão. <!--515810--> 

    > [!Tip]  
    > O ponto de atualização de software requer HTTPS porque esse é um requisito para as APIs do WSUS usadas para lidar com certificados de autenticação. Os clientes não precisam ser habilitados para HTTPS também. Para obter mais informações sobre como habilitar o HTTPS no WSUS, confira os artigos a seguir para obter assistência:  
    > - [Proteger o WSUS com o protocolo SSL](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) 
    > - [Postagem no blog de suporte do WSUS](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- Espaço em disco suficiente no ponto de atualização de software, a pasta WSUSContent, para armazenar o conteúdo binário de origem para atualizações de software de terceiros. A quantidade de armazenamento necessário varia de acordo com o fornecedor, os tipos de atualizações e as atualizações específicas que você publica para implantação. Se você precisar mover a pasta WSUSContent para outra unidade com mais espaço livre, confira a postagem no blog da equipe de suporte do WSUS [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) (Como alterar o local onde o WSUS armazena as atualizações localmente).  

- Ativar e implantar a configuração do cliente [Habilitar atualizações de software de terceiros](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates) no grupo **Atualizações de Software**.  

- O servidor do site requer acesso à Internet para download.microsoft.com pela porta HTTPS 443. O serviço de sincronização de atualização de software de terceiros é executado no servidor do site no momento. Esse serviço atualiza a lista de catálogos de terceiros disponíveis, baixa os catálogos quando você assina e baixa as atualizações quando elas são publicadas. Defina as configurações de proxy da Internet, se necessário, na guia **Proxy** das propriedades de função do Sistema de Sites no computador do servidor do site.  


### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: Habilitar e configurar o recurso
Execute as seguintes etapas *uma vez por hierarquia* para habilitar e configurar o recurso para ser usado:  

1. No console do Configuration Manager, acesse o workspace **Administração**. Expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Selecione o site de nível superior na hierarquia. Na faixa de opções, clique em **Configurar Componentes do Site** e selecione **Ponto de Atualização de Software**.  

3. Mude para a guia **Atualizações de Terceiros**. Selecione a opção para **Habilitar atualizações de software de terceiros**. Para obter mais informações sobre as opções de certificado, confira [Melhorias para habilitar o suporte de atualização de software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Se você usar a opção padrão do Configuration Manager para gerenciar esse certificado, um novo certificado do tipo **Assinatura do WSUS de Terceiros** será criado no nó **Certificados** em **Segurança** no workspace **Administração**.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: Assine um catálogo de terceiros e sincronize as atualizações
Execute as seguintes etapas para *cada catálogo de terceiros* que você deseja assinar:  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Atualizações de Software** e selecione o nó **Catálogos de Atualização de Software de Terceiros**.  

2. Selecione o catálogo a ser assinado e clique em **Assinar catálogo** na faixa de opções.   

3. Examine e aprove o certificado do catálogo.  

   > [!Note]  
   > Quando você assina um catálogo de atualizações de software de terceiros, o certificado que você examina e aprova no assistente é adicionado ao site. Esse certificado é do tipo **Catálogo de Atualizações de Software de Terceiros**. Você pode gerenciá-lo por meio do nó **Certificados** em **Segurança** no workspace **Administração**.  

4. Conclua o assistente.  

   > [!Tip]  
   > Após a assinatura inicial, o download do catálogo deverá ser iniciado imediatamente. Em seguida, ele será ressincronizado a cada 24 horas, nesta versão. Se você não quiser esperar até que o catálogo seja baixado automaticamente, clique em **Sincronizar agora** na faixa de opções.  
   > 
   > Depois que o catálogo for baixado, os metadados do produto precisarão ser sincronizados com o ponto de atualização de software. Para obter mais informações sobre esse processo e saber como iniciá-lo manualmente, confira [Sincronizar atualizações de software](/sccm/sum/get-started/synchronize-software-updates). Neste ponto, você poderá ver as atualizações de terceiros no nó **Todas as Atualizações**. 

5. Em seguida, configure os **Produtos** do ponto de atualização de software do catálogo de terceiros que você assinou. Para obter mais informações, confira [Configurar classificações e produtos para sincronização](/sccm/sum/get-started/configure-classifications-and-products). Quando houver alteração nos critérios do produto, a sincronização de atualização de software deverá ocorrer novamente.

Antes que seja possível visualizar os resultados de conformidade dos clientes, eles precisam verificar e avaliar as atualizações. Você pode disparar esse ciclo manualmente usando o painel de controle do Configuration Manager em um cliente executando a ação **Ciclo de Verificação de Atualizações de Software**. Para obter mais informações sobre o processo, confira [Introdução às atualizações de software](/sccm/sum/understand/software-updates-introduction).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: Implantar atualizações de software de terceiros
Execute as seguintes etapas para *qualquer atualização de software de terceiros* que você deseje implantar nos clientes:  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Atualizações de Software** e selecione o nó **Todas as Atualizações de Software**.  

   > [!Tip]  
   > Clique em **Adicionar Critérios** para filtrar a lista de atualizações. Por exemplo, adicione **Fornecedor** para **Adobe Systems, Inc.** para exibir todas as atualizações da Adobe.  

2. Selecione as atualizações que são necessárias para os clientes. Clique em **Publicar Conteúdo de Atualização de Software de Terceiros** e examine o andamento no SMS_ISVUPDATES_SYNCAGENT.log. Essa ação baixa os binários de atualização do fornecedor e armazena-os na pasta WSUSContent, no ponto de atualização de software. Ela também altera o estado da atualização de somente metadados para conteúdo e implantável.  

   > [!Note]  
   > Quando você publicar o conteúdo de atualização de software de terceiros, todos os certificados usados para assinar o conteúdo serão adicionados ao site. Esses certificados são do tipo **Conteúdo de Atualizações de Software de Terceiros**. Você pode gerenciá-los por meio do nó **Certificados** em **Segurança** no workspace **Administração**.  

3. Implante as atualizações usando o processo de gerenciamento de atualizações de software existente. Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates). Na página **Locais de Download** do Assistente para Implantar Atualizações de Software, selecione a opção padrão para **Baixar atualizações de software da Internet**. Nesse cenário, o conteúdo já está publicado no ponto de atualização de software, que é usado para baixar o conteúdo do pacote de implantação.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Monitorando o andamento das atualizações de software de terceiros
A sincronização de atualizações de software de terceiros é realizada pelo componente SMS_ISVUPDATES_SYNCAGENT no servidor do site. Você pode exibir as mensagens de status desse componente ou consultar um status mais detalhado no SMS_ISVUPDATES_SYNCAGENT.log. Esse log está no servidor do site na subpasta **Logs** do diretório de instalação do site. Por padrão esse caminho é `C:\Program Files\Microsoft Configuration Manager\Logs`. Para obter mais informações sobre como monitorar o processo geral de gerenciamento de atualização de software, confira [Monitorar atualizações de software](/sccm/sum/deploy-use/monitor-software-updates).


### <a name="known-issues"></a>Problemas conhecidos
- O serviço de sincronização de atualização de software de terceiros não é compatível com o ponto de atualização de software configurado para usar uma **Conta de Conexão do Servidor do WSUS**. Se essa conta estiver definida na guia **Configurações de Proxy e de Conta** da página Propriedades do Ponto de atualização de software, o seguinte erro será exibido no SMS_ISVUPDATES_SYNCAGENT.log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Para obter mais informações sobre essa conta, confira [Conta de Conexão do Ponto de Atualização de Software](/sccm/core/plan-design/hierarchy/accounts#software-update-point-connection-account).<!--515492-->  

- Não combine o uso de outras ferramentas, como o SCUP, com esse novo recurso de atualização de software de terceiros integrado. O serviço de sincronização de atualização de software de terceiros não consegue publicar conteúdo para atualizações somente de metadados adicionadas ao WSUS por outro aplicativo, ferramenta ou script, como SCUP. A ação **Publicar conteúdo de atualização de software de terceiros** falha nessas atualizações. Se você precisar implantar atualizações de terceiros que ainda não sejam compatíveis com esse recurso, use o processo existente por completo para implantar essas atualizações.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Definir as configurações do Windows Defender SmartScreen para o Microsoft Edge
<!--1353701--> Esta versão adiciona três configurações do [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) à [Política de configurações de conformidade do navegador Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). Agora, a política inclui as seguintes configurações adicionais na página **Configurações do SmartScreen**:
- **Permitir SmartScreen**: Especifica se o Windows Defender SmartScreen é permitido. Para obter mais informações, confira a [Política do navegador AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Os usuários podem substituir o aviso do SmartScreen para sites**: Especifica se os usuários podem substituir os avisos de Filtro do Windows Defender SmartScreen sobre sites potencialmente mal-intencionados. Para obter mais informações, confira a [Política do navegador PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Os usuários podem substituir o aviso do SmartScreen para arquivos**: Especifica se os usuários podem substituir os avisos de Filtro do Windows Defender SmartScreen sobre como baixar arquivos não verificados. Para obter mais informações, confira a [Política do navegador PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Sincronizar a política de MDM do Microsoft Intune para um dispositivo cogerenciado
<!--1357377--> Começando nesta versão, quando você [muda uma carga de trabalho de cogerenciamento](/sccm/core/clients/manage/co-management-switch-workloads), os dispositivos cogerenciados sincronizam a política de MDM automaticamente com o Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas Notificações do Cliente no console do Configuration Manager. Para obter mais informações, confira [Iniciar recuperação de política do cliente usando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Fazer a transição da carga de trabalho do Office 365 para o Intune usando o cogerenciamento
<!--1357841--> Agora você pode fazer a transição da carga de trabalho do Office 365 do Configuration Manager para o Microsoft Intune depois de habilitar o cogerenciamento. Para fazer a transição dessa carga de trabalho, acesse a página de propriedades de cogerenciamento e mova o controle deslizante do Configuration Manager para Piloto ou Todos. Para saber mais, confira [Cogerenciamento para dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview).

Também há uma nova condição global **Os aplicativos do Office 365 são gerenciados pelo Intune no dispositivo**. Essa condição é adicionada por padrão como um requisito dos novos aplicativos do Office 365. Ao fazer a transição dessa carga de trabalho, os clientes cogerenciados deixam de atender aos requisitos do aplicativo, portanto, não instalam o Office 365 implantado por meio do Configuration Manager.

### <a name="known-issue"></a>Problema conhecido
- A transição dessa carga de trabalho somente se aplica a implantações do Office 365 no momento. O Configuration Manager continua a gerenciar as atualizações do Office 365.<!--510876--> Para obter mais informações, inclusive uma solução alternativa, confira a nota de versão do Configuration Manager versão 1802 [A mudança da configuração do cliente Office 365 não se aplica](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861--> O Gerenciador de Conversão de Pacote agora é uma ferramenta integrada que permite converter pacotes herdados do Configuration Manager 2007 para os aplicativos do branch atual do Configuration Manager. Em seguida, você pode usar recursos de aplicativos como dependências, regras de requisitos e afinidade de dispositivo de usuário.

> [!Tip]  
> A documentação herdada da funcionalidade existente no Gerenciador de Conversão de Pacote está disponível no [TechNet](https://technet.microsoft.com/library/hh531519.aspx). A migração de informações relevantes para a biblioteca docs.microsoft.com está em andamento.

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

> [!Important]  
> Se você já tiver instalado uma versão mais antiga do Gerenciador de Conversão de Pacote, desinstale-a antes de atualizar seu site. A nova versão integrada não requer a instalação, mas pode entrar em conflito com as versões existentes.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**. Expanda **Gerenciamento de Aplicativos** e selecione **Pacotes**.  
2. Selecione um pacote. As três opções a seguir estão disponíveis no grupo **Conversão de Pacote** da faixa de opções:  
     - **Analisar Pacote**: Inicie o processo de conversão analisando o pacote.
     - **Converter Pacote**: Alguns pacotes podem ser convertidos facilmente em aplicativos com essa ação.
     - **Corrigir e Converter**: Alguns pacotes requerem que os problemas sejam corrigidos antes da conversão em aplicativos.  

   Para obter mais informações sobre essas ações, confira [Como analisar e converter pacotes](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Acesse o workspace **Monitoramento** e selecione **Status de conversão de pacote**. Esse novo painel mostra o estado geral de análise e conversão de pacotes no site. Uma nova tarefa em segundo plano resume automaticamente os dados de análise.  

   > [!Tip]  
   > O Gerenciador de Conversão de Pacote não exige o agendamento da análise de pacotes. Essa ação agora é realizada pela tarefa de resumo integrada.  

![Captura de tela do painel de status de conversão de pacote](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Implantar atualizações de software sem conteúdo
<!--1357933--> Agora você pode implantar atualizações de software em dispositivos sem precisar primeiro baixar e distribuir o conteúdo da atualização de software para os pontos de distribuição. Esse recurso será útil para lidar com um conteúdo de atualização muito grande ou quando você quiser que os clientes sempre obtenham o conteúdo por meio do serviço de nuvem do Microsoft Update. Os clientes nesse cenário também podem baixar o conteúdo de pares que já tenham o conteúdo necessário. O cliente do Configuration Manager continua a gerenciar o download de conteúdo, portanto, é possível usar o recurso de cache par do Configuration Manager ou outras tecnologias, como a Otimização de Entrega. Esse recurso permite qualquer tipo de atualização compatível com o gerenciamento de atualizações de software do Configuration Manager, incluindo as atualizações do Windows e do Office. 

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. Inicie uma implantação de atualização de software como de costume. Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).
2. No Assistente para Implantar Atualizações de Software, na página **Pacote de Implantação**, selecione a nova opção para **Nenhum pacote de implantação**.

### <a name="known-issues"></a>Problemas conhecidos
- O ícone de uma atualização implantada com essa configuração é exibido incorretamente com um X vermelho como se a atualização fosse inválida. Para obter mais informações, confira [Ícones usados para atualizações de software](/sccm/sum/understand/software-updates-icons). <!--515556-->  
- Essa configuração somente é integrada com o Assistente para Implantar Atualizações de Software. Ela não está disponível com regras de implantação automática no momento. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integração da Ferramenta de Personalização do Office com o Instalador do Office 365
<!--1358149--> A Ferramenta de Personalização do Office agora está integrada ao instalador do Office 365 no console do Configuration Manager. Ao criar uma implantação para o Office 365, agora você pode definir dinamicamente as configurações de capacidade de gerenciamento mais recentes do Office. A Ferramenta de Personalização do Office é atualizada ao mesmo tempo que o lançamento de novos builds do Office 365. Agora, você pode aproveitar as novas configurações de capacidade de gerenciamento no Office 365 assim que elas ficam disponíveis. 

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa o console do Configuration Manager precisa de acesso à Internet pela porta HTTPS 443. O Assistente de Instalação do Cliente Office 365 usa uma API do navegador da Web padrão do Windows para abrir https://config.office.com. Se um proxy da Internet for usado, será necessário que o usuário consiga acessar essa URL.

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software** e selecione o nó **Gerenciamento de Cliente Office 365**.
2. Clique o **instalador do Office 365** bloco no painel para iniciar o Assistente de instalação de cliente do Office 365. Para obter mais informações, confira [Implantar aplicativos do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).
3. Na página **Configuração do Office**, clique em **Acessar página da Web do Office**. Use a Ferramenta de Personalização do Office online para especificar as configurações dessa implantação. 
4. Clique em **Enviar** no canto superior direito ao concluir. Conclua o Assistente de Instalação do Cliente Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Melhorias no gateway de gerenciamento de nuvem
Esta versão inclui as seguintes melhorias no CMG (gateway de gerenciamento de nuvem):

### <a name="simplified-client-bootstrap-command-line"></a>Linha de comando de inicialização de cliente simplificada
<!--1358215--> Ao instalar o cliente do Configuration Manager na Internet por meio de um CMG, menos propriedades de linha de comando são necessárias agora. Para obter mais informações sobre um exemplo desse cenário, confira [Linha de comando para instalar o cliente do Configuration Manager](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) ao se preparar para o cogerenciamento. 

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

Para obter mais informações, consulte [Propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="download-content-from-a-cmg"></a>Baixar o conteúdo de um CMG
<!--1358651--> Anteriormente, era necessário implantar um ponto de distribuição na nuvem e um CMG como funções separadas. Agora, nesta versão, um CMG também pode entregar conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para habilitar esse recurso, habilite a nova opção para **Permitir que o CMG funcione como um ponto de distribuição na nuvem e entregue conteúdo do armazenamento do Azure** na guia **Configurações** das propriedades do CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>O certificado raiz confiável não é necessário com o Azure AD
<!--503899--> Ao criar um CMG, não é mais necessário fornecer um [certificado raiz confiável](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) na página Configurações. Esse certificado não é necessário ao usar o Azure AD (Azure Active Directory) para autenticação do cliente, mas costumava ser necessário no assistente.

> [!Important]  
> Se você estiver usando certificados de autenticação de cliente de PKI, ainda será necessário adicionar um certificado raiz confiável para o CMG.



## <a name="improvements-to-secure-client-communications"></a>Melhorias nas comunicações seguras com o cliente
<!--1358278,1358279--> Esta versão continua a aumentar as [melhorias nas comunicações seguras](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications) com o cliente removendo as dependências adicionais da conta de acesso à rede. Quando você habilita a nova opção do site para **Usar certificados gerados pelo Configuration Manager para os sistemas de sites HTTP**, os cenários a seguir não exigem uma conta de acesso à rede para baixar conteúdo de um ponto de distribuição:  

- Sequências de tarefas em execução da mídia de inicialização ou do PXE
- Sequências de tarefas em execução no Centro de Software  

Essas sequências de tarefas podem ser usadas para implantação de sistema operacional ou personalização. Elas também são compatíveis com computadores de grupo de trabalho.



## <a name="software-center-infrastructure-improvements"></a>Melhorias na infraestrutura do Centro de Software
<!--1358309--> Funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis ao usuário no Centro de Software. Essa alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. O Centro de Software agora depende do ponto de gerenciamento para obter essas informações, o que ajuda ambientes maiores a serem melhor dimensionados por meio de suas atribuições a [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. Remova todas as funções de catálogo de aplicativos do site. Essas funções incluem o ponto de serviço Web de catálogo de aplicativos e o ponto de site do catálogo de aplicativos.
2. Implantar um aplicativo como disponível para uma coleção de usuários.
3. Use o Centro de Software como um usuário de destino para procurar, solicitar e instalar o aplicativo.

### <a name="known-issue"></a>Problema conhecido
- Se você usar um cliente associado ao Azure Active Directory com esse recurso, não configure o site para **Usar certificados gerados pelo Configuration Manager para os sistemas de sites HTTP**. Essa opção está em conflito com esse recurso no momento.<!--515846--> Para obter mais informações sobre essa configuração, confira [melhorias nas comunicações seguras com o cliente](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Provisionar pacotes de aplicativos do Windows para todos os usuários em um dispositivo
<!--1358310--> Agora você pode provisionar um aplicativo com um pacote do aplicativo do Windows para todos os usuários no dispositivo. Um exemplo comum desse cenário é o provisionamento de um aplicativo da Microsoft Store para Empresas e Educação, como o Minecraft: Education Edition, para todos os dispositivos usados pelos alunos em uma escola. Anteriormente, o Configuration Manager somente permitia a instalação desses aplicativos por usuário. Depois de entrar em um novo dispositivo, o aluno precisava esperar para acessar um aplicativo. Agora, quando o aplicativo é provisionado no dispositivo para todos os usuários, eles podem começar a produzir mais rapidamente.

> [!Important]  
> Tenha cuidado com a instalação, o provisionamento e atualização de versões diferentes do mesmo pacote do aplicativo do Windows em um dispositivo, pois isso pode causar resultados inesperados. Esse comportamento pode ocorrer ao usar o Configuration Manager para provisionar o aplicativo, mas, em seguida, permitir que os usuários atualizem o aplicativo da Microsoft Store. Para obter mais informações, confira as diretrizes da próxima etapa ao [Gerenciar aplicativos da Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Ao provisionar um aplicativo licenciado offline, o Configuration Manager não permite que o Windows o atualize automaticamente da Microsoft Store.  

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. Crie um novo aplicativo. Esse aplicativo precisa ser de um pacote do aplicativo do Windows ou um aplicativo licenciado offline que você já sincronizou da Microsoft Store para Empresas e Educação.  

2. Na página **Informações Gerais** do Assistente para Criar Aplicativo, habilite a opção para **Provisionar este aplicativo para todos os usuários no dispositivo**.  

   > [!Tip]  
   > Se você estiver modificando um aplicativo existente, essa configuração estará na guia **Experiência do Usuário** das propriedades do aplicativo.  

3. Implante o aplicativo em uma coleção de dispositivos.  

4. Entre em um dispositivo de destino com diferentes contas de usuário e inicie o aplicativo.  

> [!Note]  
> Se você precisar desinstalar um aplicativo provisionado de dispositivos nos quais os usuários já entraram, será necessário criar duas implantações de desinstalação. Direcione a primeira implantação de desinstalação a uma coleção de dispositivos que contenha os dispositivos. Direcione a segunda implantação de desinstalação a uma coleção de usuários que contenha os usuários que já entraram nos dispositivos com o aplicativo provisionado. Quando você desinstala um aplicativo provisionado em um dispositivo, no momento, o Windows não desinstala esse aplicativo dos usuários também. 



## <a name="improvements-to-the-surface-dashboard"></a>Melhorias no painel do Surface
<!--1358654--> Esta versão inclui as seguintes melhorias ao [painel do Surface](/sccm/core/clients/manage/surface-device-dashboard):
- O painel do Surface agora exibe uma lista de dispositivos relevantes quando as seções do gráfico são selecionadas.
   - Clicar no bloco **Percentual de dispositivos do Surface** abre uma lista de dispositivos do Surface.
   - Clicar em uma barra no bloco **Cinco Principais Versões de Firmware** abre uma lista de dispositivos do Surface com essa versão de firmware específica.
- Ao exibir essas listas de dispositivo no painel do Surface, você pode clicar com o botão direito do mouse em um dispositivo e executar ações comuns.



## <a name="hardware-inventory-default-unit-revision"></a>Revisão da unidade padrão do inventário de hardware
<!--514442--> No [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), a unidade padrão usada em vários modos de exibição de relatórios foi alterada de MB (megabytes) para GB (gigabytes). Devido às [Melhoria no inventário de hardware para grandes valores inteiros](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values) e com base nos comentários dos clientes, essa unidade padrão voltou a ser MB.



## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
