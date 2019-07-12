---
title: Cache de pares do cliente
titleSuffix: Configuration Manager
description: Use o cache par do cliente como locais de fonte durante a implantação de conteúdo com o Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aadb544180d7662f1b60c73db6a35b64f8b7efe7
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676842"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache par para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1101436-->
Use o cache par para ajudar a gerenciar a implantação de conteúdo para clientes em locais remotos. O cache par é uma solução interna do Configuration Manager que o os clientes podem usar para compartilhar conteúdo com outros clientes diretamente do cache local.   

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## <a name="overview"></a>Visão geral

Definições:  

- **Cliente de cache par**: qualquer cliente do Configuration Manager que baixa o conteúdo de um par  

- **Fonte de cache par**: um cliente do Configuration Manager que você habilita para o cache par e que tem o conteúdo a ser compartilhado com outros clientes  

Use as configurações do cliente para permitir que os clientes sejam fontes de cache par. Você não precisa habilitar os clientes de cache par. Quando você permitir que os clientes sejam fontes de cache par, o ponto de gerenciamento os incluirá na lista de fontes de conteúdo local.<!--510397--> Para obter mais informações sobre esse processo, confira [Operações](#operations).  

Uma fonte de cache par precisa ser membro do grupo de limites atual do cliente de cache par. O ponto de gerenciamento não inclui fontes de cache par de um grupo de limites vizinho na lista de fontes de conteúdo, que ele fornece ao cliente. Ele inclui apenas os pontos de distribuição de um grupo de limites vizinho. Para obter mais informações sobre grupos de limite atuais e próximos, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).<!--SCCMDocs issue 685-->  

O cliente do Configuration Manager usa o cache par para fornecer todo tipo de conteúdo mantido no cache a outros clientes. Esse conteúdo inclui arquivos do Office 365 e arquivos de instalação expressa.<!--SMS.500850-->  

O cache par não substitui o uso de outras soluções, como o Windows BranchCache ou a Otimização de Entrega. O cache par funciona juntamente com outras soluções. Essas tecnologias oferecem mais opções para estender as soluções tradicionais de implantação de conteúdo, como os pontos de distribuição. O cache par é uma solução personalizada que não depende do BranchCache. Se você não habilitar nem usar o BranchCache, o cache par ainda funcionará.  

  > [!Note]  
  > A partir da versão 1802, o Windows BranchCache está sempre ativado nas implantações. A configuração para **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede** foi removida.<!--SCCMDocs issue 539--> Se o ponto de distribuição oferecer suporte e estiver habilitado nas configurações do cliente, os clientes usarão o BranchCache. Para saber mais, confira [Configurar o BranchCache](/sccm/core/clients/deploy/about-client-settings#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operações

Para habilitar o cache par, implante as [configurações do cliente](#bkmk_settings) em uma coleção. Assim, os membros dessa coleção passarão a agir como uma fonte de cache par para outros clientes no mesmo grupo de limites.  

 - Um cliente que opera como fonte de conteúdo de pares envia uma lista do conteúdo disponível armazenado em cache para o ponto de gerenciamento.  

 - Outro cliente no mesmo grupo de limites faz uma solicitação de local de conteúdo ao ponto de gerenciamento. O servidor retorna a lista de possíveis fontes de conteúdo. Essa lista inclui cada fonte de cache par que tem o conteúdo e está online. Ela também inclui os pontos de distribuição e outros locais de fonte de conteúdo nesse grupo de limites. Para obter mais informações, confira [Prioridade de fonte de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).  

 - Como de costume, o cliente que está procurando o conteúdo seleciona uma fonte na lista fornecida. O cliente tenta então obter o conteúdo.  

Da versão 1806 em diante, os grupos de limites incluem configurações adicionais para dar a você mais controle sobre a distribuição de conteúdo em seu ambiente. Para saber mais, confira [Opções de grupo de limites para downloads de pares](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Se o cliente fizer fallback para um grupo de limites vizinho para buscar o conteúdo, o ponto de gerenciamento não adicionará as fontes de cache par do grupo de limites vizinho à lista de possíveis locais de fontes de conteúdo.  

Escolha apenas os clientes mais adequados como fontes de cache par. Avalie a adequação de cliente com base em atributos como tipo de chassi, espaço em disco e conectividade de rede. Para obter mais informações que podem ajudar a selecionar os melhores clientes a serem usados para cache par, confira [este blog de um consultor da Microsoft](https://blogs.technet.microsoft.com/askpfeplat/2018/11/21/configuration-manager-peer-cache-custom-reporting-examples/).


### <a name="limited-access-to-a-peer-cache-source"></a>Acesso limitado a uma fonte de cache par  

Uma fonte de cache par rejeita as solicitações de conteúdo quando atende a uma das seguintes condições no momento em que um par solicita o conteúdo:  

  -  Modo de bateria fraca  

  -  A carga do processador excede 80%  

  -  A E/S de disco tem um *AvgDiskQueueLength* que excede 10  

  -  Não há mais conexões disponíveis com o computador  

> [!Tip]  
> Definir essas configurações usando a classe do WMI do servidor de configuração de cliente para o recurso de origem par (*SMS_WinPEPeerCacheConfig*) no SDK do Configuration Manager.  

Quando a fonte do cache par rejeita uma solicitação de conteúdo, o cliente de cache par continua a procurar o conteúdo em sua lista de locais de fonte de conteúdo.   



## <a name="requirements"></a>requisitos

- O cache par é compatível com todas as versões do Windows com suporte na lista [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Não há suporte para sistemas operacionais que não são o Windows como fontes de cache par ou clientes de cache par.  

- Uma fonte de cache par precisa ser um cliente do Configuration Manager ingressado no domínio. No entanto, um cliente que não ingressou no domínio pode obter o conteúdo de uma fonte de cache par que ingressou no domínio.  

- Os clientes só podem baixar conteúdo de fontes de cache par no grupo de limites atual.  

- Não é necessário usar uma [conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account), com a seguinte exceção:  

    - Configure uma conta de acesso à rede no site quando um cliente habilitado para cache par executar uma sequência de tarefas no Centro de Software e reinicializar a imagem de inicialização. Quando o dispositivo está no Windows PE, ele usa a conta de acesso à rede para obter o conteúdo da fonte de cache par.  

    - Quando necessário, a fonte de cache par usa a conta de acesso à rede para autenticar as solicitações de download do par. Essa conta requer somente permissões de usuário de domínio para essa finalidade.  

- Com a versão 1802 e anteriores, o último envio de descoberta de pulsação do cliente determina o limite atual de uma fonte de cache par. Um cliente que usa um perfil móvel em um grupo de limites diferente ainda pode ser membro de seu grupo de limites anterior para fins de cache par. Esse comportamento faz com que seja oferecida ao cliente uma fonte de cache par que não está em seu local de rede imediato. Não habilite a clientes que usam perfil móvel como uma fonte de cache par.<!--SCCMDocs issue 641-->  

    > [!Important]  
    > Da versão 1806 em diante, o Configuration Manager é mais eficiente em determinar se uma fonte de cache par fez roaming para outro local. Esse comportamento garante que o ponto de gerenciamento ofereça-o como uma fonte de conteúdo aos clientes no novo local, e não no local antigo. Se você estiver usando o recurso de cache par com as fontes de cache par de roaming, depois de atualizar o site para a versão 1806, também atualize todas as fontes de cache par para a versão mais recente do cliente. O ponto de gerenciamento não inclui essas fontes de cache par na lista de locais de conteúdo até que eles sejam atualizadas pelo menos para a versão 1806.<!--SCCMDocs issue 850-->  

- Antes de tentar baixar conteúdo, o ponto de gerenciamento primeiro valida que a fonte de cache par está online.<!--sms.498675--> Essa validação ocorre por meio do "canal rápido" de notificação do cliente, que usa a porta TCP 10123.<!--511673-->  

> [!Note]  
> Para aproveitar os novos recursos do Configuration Manager, primeiro atualize os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.  



## <a name="bkmk_settings"></a> Configurações do cliente de cache par

Para obter mais informações sobre as configurações do cliente de cache par, confira [Configurações de cache do cliente](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). 

Para obter mais informações de como definir essas configurações, confira [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings).

Em clientes habilitados para cache par que usam o Firewall do Windows, o Configuration Manager configura as portas do firewall que você especifica nas configurações do cliente.



## <a name="bkmk_parts"></a> Suporte para download parcial
<!--1357346-->
Começando na versão 1806, as fontes de cache de par do cliente podem dividir o conteúdo em partes. Essas partes minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gerenciamento fornece acompanhamento mais detalhado das partes do conteúdo. Ele tentará eliminar mais de um download do mesmo conteúdo por grupo de limites. 


### <a name="example-scenario"></a>Cenário de exemplo

A Contoso tem um único site primário com dois grupos de limites: HQ (Matriz) e Filial. Há uma relação de fallback de 30 minutos entre os grupos de limites. O ponto de gerenciamento e o ponto de distribuição para o site são apenas no limite do HQ. O local da filial não tem nenhum ponto de distribuição local. Dois dos quatro clientes na filial são configurados como origens de cache de par. 

![Diagrama de configuração de rede, conforme descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. Você direciona uma implantação com conteúdo para todos os quatro clientes na filial. Você distribuiu apenas o conteúdo para o ponto de distribuição.  

2. O Client3 e o Client4 não têm um local de origem para a implantação. O ponto de gerenciamento instrui os clientes a aguardarem 30 minutos antes de voltar para o grupo de limite remoto.  

3. Client1 (PCS1) é a primeira origem de cache par para atualizar a política com o ponto de gerenciamento. Como esse cliente está habilitado como uma fonte de cache par, o ponto de gerenciamento o instrui para iniciar imediatamente o download da parte A do ponto de distribuição.  

4. Quando o Client2 (PCS2) entra em contato com o ponto de gerenciamento, como a parte A já está em andamento, mas ainda não está concluída, o ponto de gerenciamento o instrui a começar a baixar imediatamente a parte B do ponto de distribuição.  

5. PCS1 conclui o download da parte A e imediatamente notifica o ponto de gerenciamento. Como parte B já está em andamento, mas ainda não está concluída, o ponto de gerenciamento o instrui a começar a baixar a parte C do ponto de distribuição.  

6. PCS2 conclui o download da parte B e imediatamente notifica o ponto de gerenciamento. O ponto de gerenciamento o instrui a começar a baixar a parte D do ponto de distribuição.  

7. PCS1 conclui o download da parte C e imediatamente notifica o ponto de gerenciamento. O ponto de gerenciamento o informa que não há mais partes disponíveis no ponto de distribuição remoto. O ponto de gerenciamento o instrui a baixar a parte B de seu par local, PCS2.  

8. Esse processo continua até que ambas as fontes de cache par do cliente tenham todas as partes uma da outra. O ponto de gerenciamento prioriza partes do ponto de distribuição remoto antes de instruir a fonte de cache par a baixar as partes dos pares locais.  

9. Client3 é o primeiro a atualizar a política após o período de 30 minutos de fallback expirar. Agora, ele verifica com o ponto de gerenciamento, que informa o cliente sobre novas fontes de locais. Em vez de baixar o conteúdo completo do ponto de distribuição na WAN, ele baixa o conteúdo completo de uma das fontes de cache par de cliente. Os clientes priorizam as fontes pares locais. 

> [!Note]  
> Se o número de fontes de cache de par de cliente for maior do que o número de partes de conteúdo, o ponto de gerenciamento instruirá as fontes de cache de par adicionais a aguardar o fallback como um cliente normal. 


### <a name="configure-partial-download"></a>Configurar o download parcial

1. Configure [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e fontes de cache par como de costume.  

2. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione **Sites**. Clique em **Configurações da hierarquia**  na faixa de opções.  

3. Na guia **Geral**, habilite a opção de **Configurar fontes de cache par de cliente para dividir o conteúdo em partes**.  

4. Crie uma implantação necessária com o conteúdo.  

   > [!Note]  
   > Essa funcionalidade só funciona quando o cliente baixa o conteúdo em segundo plano, como com uma implantação necessária. Os downloads de sob demanda, como quando o usuário instala uma implantação disponível no Centro de Software, se comportam como de costume.  

Para vê-los tratando o download do conteúdo em partes, examine o **ContentTransferManager.log** na fonte de cache par do cliente e o **MP_Location.log** no ponto de gerenciamento.  



## <a name="guidance-for-cache-management"></a>Diretrizes para gerenciamento de cache
<!--510645-->
O cache par baseia-se no cache do cliente do Configuration Manager para compartilhar o conteúdo. Considere os pontos a seguir para gerenciar o cache do cliente em seu ambiente:  

- O cache do cliente do Configuration Manager não é como a biblioteca de conteúdo em um ponto de distribuição. Enquanto você gerencia o conteúdo que você distribui para um ponto de distribuição, o cliente do Configuration Manager gerencia automaticamente o conteúdo em seu cache. Há definições e métodos para ajudar a controlar qual conteúdo fica no cache de uma fonte de cache par. Para obter mais informações, confira [Configurar o cache do cliente para clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

- O tamanho e a manutenção normais do cache aplicam-se às fontes de cache par. Para obter mais informações, confira [Configurar o tamanho do cache do cliente](/sccm/core/clients/deploy/about-client-settings#configure-client-cache-size). Considere o tamanho de um conteúdo maior, como pacotes de atualização de sistema operacional ou arquivos de atualização expressa do Windows 10. Compare a necessidade que você tem de obter esse conteúdo em relação ao espaço em disco disponível nas fontes de cache par.  

- O cliente da fonte de cache par atualiza o horário da última referência ao conteúdo no cache quando um par o baixa. O cliente usa esse carimbo de data/hora quando mantém automaticamente seu cache, removendo o conteúdo mais antigo primeiro. Portanto, ele deve esperar para remover o conteúdo que os clientes do cache par mais baixam, caso haja algum.  

- Se necessário, durante uma sequência de tarefas de implantação de sistema operacional, use a variável **SMSTSPreserveContent** para manter o conteúdo no cache do cliente. Para saber mais, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSPreserveContent).  

- Se necessário, ao criar o software a seguir, use a opção para **Persistir conteúdo no cache do cliente**:  
    - Aplicativos
    - Pacotes
    - Imagens do sistema operacional
    - Pacotes de atualização do sistema operacional
    - Imagens de inicialização



## <a name="monitoring"></a>monitoramento   

Para ajudá-lo a entender o uso do cache par, exiba o painel **Fontes de Dados do Cliente**. Para obter mais informações, confira [Painel de fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Além disso, use relatórios para exibir o uso do cache par. No console, acesse o workspace **Monitoramento**, expanda **Relatório** e selecione o nó **Relatórios**. Todos os seguintes relatórios têm o tipo **Conteúdo de Distribuição de Software**:  

1.  **Rejeição de conteúdo de origem de cache de pares**: com que frequência as fontes de cache de pares em um grupo de limites rejeitam uma solicitação de conteúdo.  

    > [!Note]  
    > **Problema conhecido**<!--486652-->: ao fazer uma busca detalhada nos resultados, como *MaxCPULoad* ou *MaxDiskIO*, você pode receber um erro que sugere que o relatório ou seus detalhes não podem ser encontrados. Para solucionar esse problema, use os outros dois relatórios que mostram os resultados diretamente.  

2. **Rejeição de conteúdo de origem do cache de pares por condição**: mostra os detalhes de rejeição para um grupo de limites ou tipo de rejeição especificado. 

    > [!Note]  
    > **Problema conhecido**<!--486652-->: não é possível selecionar os parâmetros disponíveis; é preciso digitá-los manualmente. Insira os valores de *Nome do Grupo de Limites* e *Tipo de Rejeição* como visto no relatório **Rejeição de conteúdo de fonte de cache par**. Por exemplo, para *Tipo de Rejeição*, você pode inserir *MaxCPULoad* ou *MaxDiskIO*.  

3. **Detalhes da rejeição de conteúdo de origem de cache de pares**: mostra o conteúdo que o cliente estava solicitando quando ele foi rejeitado.  

    > [!Note]  
    > **Problema conhecido**<!--486652-->: não é possível selecionar os parâmetros disponíveis; é preciso digitá-los manualmente. Insira o valor para *Tipo de Rejeição* conforme exibido no relatório de **Rejeição do conteúdo de origem do cache par**. Em seguida, digite a *ID de Recurso* para a fonte de conteúdo sobre a qual você deseja obter mais informações. 
    > 
    > Para localizar a ID de recurso da fonte de conteúdo:  
    > 
    > 1. Localizar o nome do computador que é exibido como a *Origem de cache par* nos resultados da **Rejeição de conteúdo de fonte de cache par por condição**.  
    > 
    > 2. Acesse o workspace **Ativos e Conformidade**, selecione o nó **Dispositivos** e pesquise o nome do computador. Use o valor da coluna de ID de Recurso.  

