---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis no Technical Preview do Configuration Manager versão 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4735678e9a6a42dedc676a8a0223af0ac8d6b81b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135898"
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1803 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do Configuration Manager, versão 1803. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Technical Preview. 

Examine o artigo de [Technical Preview](/sccm/core/get-started/technical-preview) antes de instalar essa atualização. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Os pontos de distribuição por pull são compatíveis com os pontos de distribuição de nuvem como origem  
<!--1321554--> Muitos clientes usam [pontos de distribuição de pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) em escritórios remotos ou filiais, que baixam o conteúdo de um ponto de distribuição de origem pela WAN. Se seus escritórios remotos tiverem uma conexão melhor com a Internet ou para reduzir a carga em seus links de WAN, agora você poderá usar um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) no Microsoft Azure como a origem. Quando você adiciona uma fonte na guia **Ponto de distribuição por pull** das propriedades do ponto de distribuição, qualquer ponto de distribuição de nuvem no site agora é listado como um ponto de distribuição disponível. O comportamento de ambas as funções do sistema de sites permanece o mesmo caso contrário. 

### <a name="prerequisites"></a>Pré-requisitos
- O ponto de distribuição por pull precisa de acesso à Internet para se comunicar com o Microsoft Azure.
- O conteúdo deve ser distribuído para o ponto de distribuição da nuvem de origem.

> [!Note]  
> Esse recurso pode incorrer em encargos para sua assinatura do Azure para armazenamento e rede para saída de dados. Para obter mais informações, consulte o custo do uso da [distribuição baseada em nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_CloudDPCost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>O suporte parcial de download no cache de par de cliente para reduzir a utilização de WAN
<!--1357346--> As fontes de cache de par de cliente agora podem dividir o conteúdo em partes. Essas partes minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gerenciamento fornece acompanhamento mais detalhado das partes do conteúdo. Ele tentará eliminar mais de um download do mesmo conteúdo por grupo de limites. 

### <a name="example-scenario"></a>Cenário de exemplo
A Contoso tem um único site primário com dois grupos de limites: HQ (Matriz) e Filial. Há uma relação de fallback de 30 minutos entre os grupos de limites. O ponto de gerenciamento e o ponto de distribuição para o site são apenas no limite do HQ. O local da filial não tem nenhum ponto de distribuição local. Dois dos quatro clientes na filial são configurados como origens de cache de par. 

![Diagrama de configuração de rede, conforme descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. Você direciona uma implantação com conteúdo para todos os quatro clientes na filial. Você distribuiu apenas o conteúdo para o ponto de distribuição.
2. Client3 e Client4 não tem um local de origem para a implantação. O ponto de gerenciamento instrui os clientes a aguardarem 30 minutos antes de voltar para o grupo de limite remoto.
3. Client1 (PCS1) é a primeira origem de cache par para atualizar a política com o ponto de gerenciamento. Como esse cliente está habilitado como uma fonte de cache par, o ponto de gerenciamento o instrui para iniciar imediatamente o download da parte A do ponto de distribuição.  
4. Quando o Client2 (PCS2) entra em contato com o ponto de gerenciamento, como a parte A já está em andamento, mas ainda não está concluída, o ponto de gerenciamento o instrui a começar a baixar imediatamente a parte B do ponto de distribuição.
5. PCS1 conclui o download da parte A e imediatamente notifica o ponto de gerenciamento. Como parte B já está em andamento, mas ainda não está concluída, o ponto de gerenciamento o instrui a começar a baixar a parte C do ponto de distribuição.
6. PCS2 conclui o download da parte B e imediatamente notifica o ponto de gerenciamento. O ponto de gerenciamento o instrui a começar a baixar a parte D do ponto de distribuição. 
7. PCS1 conclui o download da parte C e imediatamente notifica o ponto de gerenciamento. O ponto de gerenciamento o informa que não há mais partes disponíveis no ponto de distribuição remoto. O ponto de gerenciamento o instrui a baixar a parte B de seu par local, PCS2.
8. Esse processo continua até que ambas as fontes de cache par do cliente tenham todas as partes uma da outra. O ponto de gerenciamento prioriza partes do ponto de distribuição remoto antes de instruir a fonte de cache par a baixar as partes dos pares locais. 
9. Client3 é o primeiro a atualizar a política após o período de 30 minutos de fallback expirar. Agora, ele verifica com o ponto de gerenciamento, que informa o cliente sobre novas fontes de locais. Em vez de baixar o conteúdo completo do ponto de distribuição na WAN, ele baixa o conteúdo completo de uma das fontes de cache par de cliente. Os clientes priorizam as fontes pares locais. 

> [!Note]  
> Se o número de fontes de cache de par de cliente for maior do que o número de partes de conteúdo, o ponto de gerenciamento instruirá as fontes de cache de par adicionais a aguardar o fallback como um cliente normal. 


### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. Configure [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e [fontes de cache par](/sccm/core/plan-design/hierarchy/client-peer-cache) como normalmente.
2. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione **Sites**. Clique em **Configurações da hierarquia**  na faixa de opções. 
3. Na guia **Geral**, habilite a opção de **Configurar fontes de cache par de cliente para dividir o conteúdo em partes**. 
4. Crie uma implantação necessária com o conteúdo.  

   > [!Note]  
   > Essa funcionalidade só funciona quando o cliente baixa o conteúdo em segundo plano, como com uma implantação necessária. Os downloads de sob demanda, como quando o usuário instala uma implantação disponível no Centro de Software, se comportam como de costume.  

1. Para vê-los tratando o download do conteúdo em partes, examine o **ContentTransferManager.log** na fonte de cache par do cliente e o **MP_Location.log** no ponto de gerenciamento.  
 



## <a name="maintenance-windows-in-software-center"></a>Janelas de manutenção no Centro de Software
<!--1358131--> O Centro de Software agora exibe a próxima janela de manutenção agendada. Na guia Status da Instalação, alterne a exibição de Todas os para Futuras. Isso exibe o intervalo de tempo e a lista de implantações que estão agendadas. A lista estará em branco se não houver nenhuma janela de manutenção futura. 

![Centro de Software mostrando a lista de implantações futuras na guia Status da Instalação](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Guia personalizada para página da Web no Centro de Software
<!--1358132--> Agora você pode criar uma guia personalizada para abrir uma página da Web no Centro de Software. Esse recurso permite que você mostre conteúdo aos usuários finais de forma consistente e confiável. A lista a seguir inclui alguns exemplos:
- Entrar em contato com TI: informações sobre como entrar em contato com o departamento de TI da sua organização
- Centro de Suporte de TI: ações de autoatendimento de TI, como a pesquisa em uma base de dados de conhecimento ou a abertura de um tíquete de suporte.
- Documentação do usuário final: artigos para usuários em sua organização em vários tópicos de TI, por exemplo, usar aplicativos ou atualizar para o Windows 10.


### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No console do Configuration Manager, no workspace **Administração**, no nó **Configurações do Cliente**, abra a política **Configurações do Cliente Padrão**.
2. Selecione o grupo **Centro de Software**.
3. Para **Configurações do Centro de Software**, clique em **Personalizar**.
4. Alterne para a guia **Guias**.
5. Habilite a opção **Especificar uma guia personalizada para o Centro de Software**.
    1. Insira um nome no campo de texto **Nome da guia** campo de texto. Esse nome é o exibido para o usuário no Centro de Software.
    2. Insira uma URL válida no campo de texto **URL de Conteúdo**. Essa URL é o conteúdo que o Centro de Software exibe quando os usuários clicam nessa guia.

> [!Tip]  
> O Centro de Software usa componentes do Internet Explorer para renderizar a página da Web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Habilitar o suporte de atualização de software de terceiros em clientes

Agora você pode habilitar a configuração de clientes do Configuration Manager para atualizações de software de terceiros. Quando você **habilitar as atualizações de software de terceiros** nas propriedades de componente de SUP, o SUP baixará o certificado de autenticação usado pelo WSUS para atualizações de terceiros. <!--1357605-->

Selecionar **Habilitar atualizações de software de terceiros** nas configurações do cliente faz o seguinte: 
- No cliente, ele define a política para ‘Permitir assinaturas assinadas para um local de serviço de atualização da Microsoft da intranet’ 
- Instala o certificado de autenticação para o repositório Fornecedores Confiáveis no cliente. 

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No site de nível superior na hierarquia do Configuration Manager, vá para o nó **Administração**, expanda **Configuração do Site** e, em seguida, **Sites**.
2. Clique com o botão direito do mouse no servidor do site de nível superior e selecione **Configurar Componentes do Site**, em seguida, **Ponto de Atualização de Software**.
3. Clique na guia **Atualizações de Terceiros** e marque a opção **Habilitar atualizações de software de terceiros**.
4. Abra **Configurações do Cliente** e vá para as configurações de **Atualizações de Software**.
5. Certifique-se de que **Habilitar atualizações de software de terceiros** esteja definido como **Sim**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Habilitar copiar/colar de detalhes do ativo das exibições de monitoramento
Como resultado de seus [comentários do usuário](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det), agora você pode habilitar a funcionalidade de copiar/colar no painel de detalhes do ativo nas exibições de monitoramento de status de implantação e distribuição.  <!--1357552-->

## <a name="scap-extensions"></a>Extensões do SCAP
A versão de pré-lançamento de Extensões do SCAP está disponível na pasta Cd.latest em SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Esta versão de pré-lançamento das extensões do SCAP pode ser instalada em todas as versões compatíveis no momento do branch atual do Configuration Manager e o LTSB 1606. Para obter mais informações, veja [Sobre as extensões do protocolo SCAP (Security Content Automation Protocol)](/sccm/compliance/plan-design/scap/about-scap).



## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
