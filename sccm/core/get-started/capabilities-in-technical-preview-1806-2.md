---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis na visualização técnica 1806.2 do Configuration Manager.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef015f755a42ff113b2ca80bcc2a5650fbf30231
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134734"
---
# <a name="capabilities-in-technical-preview-18062-for-system-center-configuration-manager"></a>Funcionalidades na visualização técnica 1806.2 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do Configuration Manager, versão 1806.2. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Technical Preview. 

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

### <a name="ki_sqlncli"></a> Os clientes não serão atualizados automaticamente
<!--518760--> Ao atualizar para a versão 1806.2, o site também atualiza o SQL Native Client, o que pode causar uma reinicialização pendente no servidor do site. Esse atraso faz com que determinados arquivos não sejam atualizados, o que afeta a atualização automática do cliente.

#### <a name="workarounds"></a>Soluções Alternativas
Evite esse problema atualizando manualmente o SQL Native Client *antes de atualizar* o Configuration Manager para a versão 1806.2. Para saber mais, confira [atualização de serviço mais recente do SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Se você já tiver atualizado seu site, a atualização automática do cliente e o cliente por push não funcionarão. Você precisa atualizar os clientes para testar totalmente a maioria dos novos recursos. Atualize manualmente os clientes de technical preview usando o seguinte processo:  

1. Localize os arquivos de origem do cliente na pasta **CMUClient** do diretório de instalação do Configuration Manager no servidor do site. Por exemplo, `C:\Program Files\Configuration Manager\CMUClient`  

2. Copie toda a pasta CMUClient para o dispositivo do cliente. Por exemplo, `C:\Temp\CMUClient`  

    Esse local pode ser um compartilhamento de rede acessível dos clientes.  

3. Execute a seguinte linha de comando de um prompt de comandos com privilégios elevados: `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Se você estiver instalando um novo cliente em seu site de technical preview versão 1806.2, use esse mesmo processo. 

> [!Important]  
> Não use o parâmetro de linha de comando `/MP` neste cenário. Esse parâmetro tem prioridade sobre `/source` e faz com que ccmsetup baixe conteúdo do cliente do ponto de gerenciamento ou do ponto de distribuição.
> 
> Propriedades de linha de comando, como SMSSITECODE ou CCMLOGLEVEL=3, podem ser usadas, mas não devem ser necessárias ao atualizar um cliente existente. 


### <a name="ki_version"></a> A versão 1806.2 mostra a versão 1806 em Sobre o Configuration Manager
<!--518148--> Depois de atualizar para a versão technical preview 1806.2, se você abrir a janela **Sobre o Configuration Manager** do canto superior esquerdo do console, ele ainda aparecerá como **Versão 1806**. 

#### <a name="workaround"></a>Solução alternativa
Use a propriedade **Versão do site** para determinar a diferença entre 1806 e 1806.2:

| Versão do site  | Version
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  


## <a name="bkmk_pod"></a> Melhorias para implantações em fases

Esta versão inclui as seguintes melhorias nas [implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence):
- [Status da implantação em fases](#bkmk_pod-monitor)
- [Implantação em fases de aplicativos](#bkmk_pod-app)
- [Distribuição gradual durante as implantações em fases](#bkmk_pod-throttle)


### <a name="bkmk_pod-monitor"></a> Status da implantação em fases
<!--1358577--> As implantações em fases agora têm uma experiência de monitoramento nativa. No nó **Implantações** no workspace **Monitoramento**, selecione uma implantação em fases e clique em **Status da Implantação em Fases** na faixa de opções.

![Painel de status de implantação em fases, mostrando o status de duas fases](media/1358577-phased-deployment-status.png)

Este painel mostra as seguintes informações para cada fase da implantação:  

- **Total de dispositivos**: o número de dispositivos afetados por essa fase.  

- **Status**: o status atual dessa fase. Cada fase pode estar em um dos seguintes estados:  

    - **Implantação criada**: a implantação em fases criou uma implantação do software para a coleção para essa fase. Os clientes são direcionados ativamente com este software.  

    - **Aguardando**: a fase anterior ainda não atingiu os critérios de êxito para que a implantação continue nessa fase.  

    - **Suspenso**: um administrador suspendeu a implantação.  

- **Progresso**: os estados de implantação codificados por cores dos clientes. Por exemplo: Êxito, Em Andamento, Erro, Requisitos Não Atendidos e Desconhecido. 


#### <a name="known-issue"></a>Problema conhecido
O painel de status de implantação em fases pode mostrar várias linhas para a mesma fase.<!--518510-->


### <a name="bkmk_pod-app"></a> Implantação em fases de aplicativos
<!--1358147--> Crie implantações em fases para aplicativos. As implantações em fases permitem que você coordene uma distribuição coordenada e sequenciada do software com base em grupos e critérios personalizáveis.

No console do Configuration Manager, vá para a **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione **Aplicativos**. Selecione um aplicativo e clique em **Criar Implantação em Fases** na faixa de opções. 

O comportamento de uma implantação de aplicativo em fases é igual ao de sequências de tarefas. Para saber mais, confira [Criar implantações em fases para uma sequência de tarefas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="prerequisite"></a>Pré-requisito
Distribua o conteúdo para o aplicativo para um ponto de distribuição antes de criar a implantação em fases.<!--518293-->

#### <a name="known-issue"></a>Problema conhecido
Você não pode criar manualmente as fases para um aplicativo. O assistente cria automaticamente duas fases para implantações de aplicativos.


### <a name="bkmk_pod-throttle"></a> Distribuição gradual durante as implantações em fases
<!--1358578--> Durante uma implantação em fases, a distribuição em cada fase agora pode acontecer gradualmente. Esse comportamento ajuda a reduzir o risco de problemas de implantação e diminui a carga na rede causada pela distribuição de conteúdo aos clientes. O site pode tornar gradualmente o software disponível, dependendo da configuração de cada fase. Todos os clientes em uma fase têm um prazo em relação à hora em que o software é disponibilizado. A janela entre o horário disponível e o prazo final é a mesma para todos os clientes em uma fase. 

Quando você criar uma implantação em fases e configurar manualmente uma fase na página **Configurações de Fase** do Assistente de Adição de Fase ou na página **Configurações** do assistente de Criação de Implantação em Fases, configure a opção: **Disponibilizar esse software gradualmente durante este período de tempo (em dias)**. O valor padrão dessa configuração é **0**. Portanto, por padrão, a implantação não é limitada.

> [!Note]  
> Essa opção só está disponível para implantações em fases de sequências de tarefas.  



## <a name="bkmk_msix"></a> Suporte para novos formatos do pacote de aplicativo do Windows
<!--1357427--> O Configuration Manager agora dá suporte à implantação do novo pacote de aplicativo do Windows 10 (.msix) e formatos do pacote de aplicativo (.msixbundle). Os builds mais recentes do [Windows Insider Preview](https://insider.windows.com/) atualmente dão suporte a esses novos formatos.

Para obter uma visão geral do MSIX, confira [Visão detalhada do MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Para saber como criar um novo aplicativo MSIX, confira [Suporte a MSIX introduzido no Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Pré-requisitos
- Um cliente do Windows 10 executando pelo menos o Windows Insider Preview build 17682
- Um pacote de aplicativo do Windows no formato MSIX

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, [crie um aplicativo](/sccm/apps/deploy-use/create-applications). 
2. Escolha o **Tipo** do arquivo de instalação de aplicativo como **Pacote de aplicativo do Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**.
3. [Implantar o aplicativo](/sccm/apps/deploy-use/deploy-applications) no cliente executando o build mais recente do Windows Insider Preview.



## <a name="bkmk_client-push"></a> Melhoria de segurança do cliente por push
<!--1358204--> Ao usar o método [cliente por push](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation) de instalação do cliente do Configuration Manager, o servidor de site cria uma conexão remota para o cliente para iniciar a instalação. A partir desta versão, o site pode exigir autenticação mútua do Kerberos não permitindo fallback para NTLM antes de estabelecer a conexão. Essa melhoria ajuda a proteger a comunicação entre o servidor e o cliente. 

Dependendo das políticas de segurança, seu ambiente pode já preferir ou exigir Kerberos em vez da autenticação NTLM mais antiga. Para saber mais sobre as considerações de segurança desses protocolos de autenticação, confira [Configuração de política de segurança do Windows para restringir o NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Pré-requisito

Para usar esse recurso, os clientes devem estar em uma floresta confiável do Active Directory. O Kerberos no Windows depende do Active Directory para autenticação mútua. 


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

Quando você atualiza o site, o comportamento existente persiste. Depois que você *abrir* as propriedades de instalação do cliente por push, o site habilitará automaticamente a verificação Kerberos. Se necessário, você pode permitir que a conexão realize fallback para usar uma conexão NTLM menos segura, o que não é recomendado. 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione **Sites**. Selecione o site de destino. Na faixa de opções, clique em **Configurações de Instalação do Cliente** e selecione **Instalação do Cliente por Push**.  

2. Agora, o site habilitou a verificação de Kerberos para o cliente por push. Clique em **OK** para fechar a janela.  

3. Se for necessário para seu ambiente, na janela Propriedades de Instalação por Push do Cliente, na guia **Geral**, confira a opção **Permitir fallback de conexão para NTLM**. Essa opção é desabilitada por padrão. 



## <a name="bkmk_insights"></a> Insights de gerenciamento para manutenção proativa
<!--1352184,et al--> Insights de gerenciamento adicionais estão disponíveis nesta versão para realçar os possíveis problemas de configuração. Examine as seguintes regras no novo grupo **Manutenção Proativa**:  

- **Itens de configuração não usados**: itens de configuração que não fazem parte de uma linha de base de configuração e têm mais de 30 dias.  

- **Imagens de inicialização não usadas**: imagens de inicialização não referenciadas para uso em sequência de tarefas ou inicialização PXE.  

- **Grupos de limites sem sistemas de sites atribuídos**: sem sistemas de sites atribuídos, os grupos de limites só podem ser usados para atribuição de site.  

- **Grupos de limites sem membros**: grupos de limites não serão aplicáveis para a pesquisa de conteúdo ou a atribuição de site se não tiverem membros.  

- **Pontos de distribuição que não fornecem conteúdo a clientes**: pontos de distribuição que não forneceram conteúdo aos clientes nos últimos 30 dias. Esses dados se baseiam nos relatórios de clientes de seu histórico de download.  

- **Atualizações expiradas encontradas**: as atualizações expiradas não são aplicáveis à implantação.   



## <a name="bkmk_comgmt"></a> Carga de trabalho de aplicativos móveis de transição para dispositivos cogerenciados
<!--1357892--> Gerencie aplicativos móveis com o Microsoft Intune e continue usando o Configuration Manager para implantar aplicativos da área de trabalho do Windows. Para fazer a transição da carga de trabalho de aplicativos modernos, acesse a página de propriedades de cogerenciamento. Mova o controle deslizante do Configuration Manager para Piloto ou Todos. 

Após a transição dessa carga de trabalho, todos os aplicativos disponíveis implantados do Intune estão disponíveis no Portal da Empresa. Os aplicativos que você implanta do Configuration Manager estão disponíveis no Centro de Software. 

Para obter mais informações, consulte os seguintes artigos:  

- [Cogerenciamento de dispositivos Windows 10](/sccm/core/clients/manage/co-management-overview)  

- [O que é o gerenciamento de aplicativo do Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="bkmk_bgoptions"></a> Opções de grupo de limites para downloads de pares
<!--1356193--> Os grupos de limites agora incluem configurações adicionais para dar a você mais controle sobre a distribuição de conteúdo em seu ambiente. Esta versão adiciona as seguintes opções:  

- **Permitir downloads de par nesse grupo de limites**: Essa configuração é habilitada por padrão. O ponto de gerenciamento fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Há dois cenários comuns em que você deve considerar a desabilitação dessa opção:  

    - Se você tiver um grupo de limites que inclua limites de locais geograficamente dispersos, como uma VPN. Dois clientes podem estar no mesmo grupo de limites, pois estão conectados por meio de VPN, mas em locais muito diferentes que são inadequados para o compartilhamento de conteúdo de pares.  

    - Se você usar um grupo de limites único e grande para a atribuição de site que não faça referência a nenhum ponto de distribuição.  

- **Durante o download de par, usar apenas pares dentro da mesma sub-rede**: Essa configuração depende do que foi mostrado acima. Se você habilitar essa opção, o ponto de gerenciamento incluirá apenas as origens de pares de lista do local do conteúdo que estão na mesma sub-rede que o cliente.

    Cenários comuns para habilitar essa opção:

    - O design de grupo de limites para distribuição de conteúdo inclui um grupo de limites grandes que se sobrepõe a outros grupos de limites menores. Com essa nova configuração, a lista de fontes de conteúdo que o ponto de gerenciamento fornece aos clientes inclui apenas as fontes de pares da mesma sub-rede.

    - Você tem um grupo de limites grande e único para todos os locais remotos. Habilite esta opção e os clientes só compartilharão conteúdo dentro da sub-rede no local remoto, em vez de colocar em risco o compartilhamento de conteúdo entre os locais.


### <a name="known-issue"></a>Problema conhecido
Se o cliente do código-fonte par tiver mais de um endereço IP (IPv4, IPv6 ou ambos), o cache de pares não funcionará. A nova opção, **Durante os downloads de pares, use apenas pares na mesma sub-rede**, não terá efeito se a fonte de mesmo nível tiver mais de um endereço IP.<!--518661-->   



## <a name="bkmk_3pupdate"></a> Suporte a catálogos personalizados de atualizações de software de terceiros
<!--1358714--> Essa versão aumenta ainda mais o suporte para atualizações de software de terceiros, como resultado de seus [comentários no UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). A [versão Technical Preview 1806](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate) forneceu suporte para *catálogos de parceiros*, que são catálogos registrados de fornecedores de software. Os catálogos que você fornece, que não estão registrados com a Microsoft, são chamados de *catálogos personalizados*. Adicione catálogos personalizados no console do Configuration Manager.  


### <a name="prerequisites"></a>Pré-requisitos 

- Configurar [atualizações de software de terceiros](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate). Concluir a Fase 1: Habilitar e configurar o recurso.   

- Um catálogo personalizado assinado digitalmente que contém atualizações de software assinadas digitalmente.  

- O administrador requer as seguintes permissões:  

    - Site: criar, modificar  


### <a name="try-it-out"></a>Experimente!

Tente concluir as tarefas. Depois, envie seus [comentários](capabilities-in-technical-preview-1804.md#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, vá para o workspace **Biblioteca de Software**, expanda **Atualizações de Software** e selecione o nó **Catálogos de Atualizações de Software de Terceiros**. Clique em **Adicionar Catálogo Personalizado** na faixa de opções.  

2. Na página **Geral** , especifique os seguintes detalhes:  

    - **URL de download**: Um endereço HTTPS válido do catálogo personalizado.  

    - **Publicador**: O nome da organização que publica o catálogo.  

    - **Nome**: o nome do catálogo a ser exibido no console do Configuration Manager.  

    - **Descrição**: Uma descrição do catálogo.  

    - **URL de suporte** (opcional): Um endereço HTTPS válido de um site para obter ajuda com o catálogo.  

    - **Contato de suporte** (opcional): Informações de contato para obter ajuda com o catálogo.  

3. Conclua o assistente. O assistente adiciona o novo catálogo em um estado de assinatura cancelada.  

4. Assine o catálogo personalizado usando a ação existente **Assinar o Catálogo**. Para obter mais informações, confira [Fase 2: Assinar um catálogo de terceiros e sincronizar as atualizações](/sccm/core/get-started/capabilities-in-technical-preview-1806#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Não é possível adicionar catálogos com a mesma URL de download, e você não pode editar as propriedades do catálogo. Se você especificar propriedades incorretas para um catálogo personalizado, exclua o catálogo antes de adicioná-lo novamente.  


#### <a name="unsubscribe-from-a-catalog"></a>Cancelar assinatura de um catálogo
Para cancelar a assinatura de um catálogo, selecione o catálogo desejado na lista e clique em **Cancelar a Assinatura do Catálogo** na faixa de opções. Se você cancelar a assinatura de um catálogo, as ações e os comportamentos a seguir ocorrerão: 
- O site interrompe a sincronização de novas atualizações 
- O site bloqueia os certificados associados para assinatura de catálogo e atualização de conteúdo. 
- As atualizações não são removidas, mas você não poderá publicá-las nem implantá-las.

#### <a name="delete-a-custom-catalog"></a>Excluir um catálogo personalizado
Exclua catálogos personalizados do mesmo nó do console. Selecione um catálogo personalizado em um estado *cancelado* e clique em **Excluir Catálogo Personalizado**. Se você já se inscreveu no catálogo, primeiro cancele a assinatura antes de excluí-la. Você não pode excluir catálogos de parceiros. Excluir um catálogo personalizado o remove da lista de catálogos. Essa ação não afeta as atualizações de software que você publicou para seu ponto de atualização de software.


### <a name="known-issue"></a>Problema conhecido
A ação de exclusão em catálogos personalizados está esmaecida, assim, você não pode excluir catálogos personalizados no console. Para solucionar esse problema, use a ferramenta **wbemtest** no servidor do site. Consulte a instância que você deseja excluir com o nome ou a URL de download, por exemplo: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Na janela de resultados de consulta, selecione o objeto e clique em **Excluir**.<!--518676-->  



## <a name="bkmk_cloud"></a> Melhorias nos recursos de gerenciamento de nuvem

Esta versão inclui os seguintes aprimoramentos:  

- Os recursos a seguir agora dão suporte ao uso Azure EUA Nuvem de governo:<!--511980-->  

    - Integração do site para **Gerenciamento de Nuvem** por meio dos [Serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  

    - Implantando um [gateway de gerenciamento de nuvem com o Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)  

    - Implantando um [ponto de distribuição na nuvem com o Azure Resource Manager](/sccm/core/get-started/capabilities-in-technical-preview-1805#cloud-distribution-point-support-for-azure-resource-manager)  

- Os clientes estão usando o Windows AutoPilot para provisionar o Windows 10 em dispositivos unidos ao Azure Active Directory que estão conectados à rede local. Para instalar ou atualizar o cliente do Configuration Manager nesses dispositivos, agora você não precisa de um ponto de distribuição de nuvem ou um ponto de distribuição local configurado para **permitir que os clientes se conectem anonimamente**. Em vez disso, habilite a opção de site para **Usar certificados gerados pelo Configuration Manager para sistemas de sites HTTP**, que permite que um cliente associado ao domínio de nuvem se comunique com um ponto de distribuição habilitado para HTTP local. Para saber mais, confira [melhorias nas comunicações seguras com o cliente](https://docs.microsoft.com/en-us/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="bkmk_report"></a> Novo relatório de conformidade de atualizações de software
<!--1357775--> A exibição da conformidade de relatórios de atualizações de software tradicionalmente inclui dados de clientes que não entraram em contato com o site recentemente. Um novo relatório permite filtrar os resultados de conformidade para um grupo de atualização de software específico por clientes "íntegros". Este relatório mostra o estado de conformidade mais realista de clientes ativos em seu ambiente. 
 
Para exibir o relatório, vá para o workspace **Monitoramento**, expanda **Relatórios**, expanda **Relatórios**, expanda **Atualizações de Software – Conformidade** e selecione **Conformidade 9 - Integridade geral e conformidade**. Especifique o **Grupo de Atualização**, o **Nome da Coleção** e o estado de **Integridade do Cliente**.

O relatório inclui as seguintes partes:
- **Clientes Íntegros versus Total de Clientes**: esse gráfico de barras compara os clientes "íntegros" que se comunicaram com o site no período de tempo especificado em relação ao número total de clientes na coleção especificada.
- **Visão geral de conformidade**: esse gráfico de pizza mostra o estado de conformidade geral do grupo de atualização de software específico em clientes ativos na coleção especificada.
- **Cinco principais fora de conformidade por ID do artigo**: esse gráfico de barras exibe as cinco principais atualizações de software no grupo especificado que estão fora de conformidade em clientes ativos na coleção especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.



## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
