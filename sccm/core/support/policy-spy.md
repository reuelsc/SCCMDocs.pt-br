---
title: Policy Spy
titleSuffix: Configuration Manager
description: Use o Policy Spy para exibir e solucionar problemas do sistema de política em clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 740dda5c41c28e1648eb24e75fe24a2e22784f3b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129095"
---
# <a name="policy-spy"></a>Policy Spy

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Policy Spy é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma ferramenta para exibir e solução de problemas de sistema de política em clientes do Configuration Manager. Execute **PolicySpy.exe** para abrir a interface do usuário. Para obter mais informações sobre o uso de linha de comando, veja [Sintaxe de linha de comando](#bkmk_policyspy-syntax).

> [!Important]  
> Execute o Policy Spy como administrador. Se você não **Executar como administrador**, verá o seguinte erro nas Informações do Cliente:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> Sintaxe da linha de comando

O Policy Spy destina-se principalmente a uso por meio de sua interface do usuário. Ele oferece opções de linha de comando limitadas para dar suporte à automação e ao processamento em lote.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Opção: `/export`
Essa opção exporta silenciosamente a política do computador local ou remoto. `<ExportFilename>` é o nome do arquivo para o qual a ferramenta salva a política exportada para XML. Se você especificar a opção `<computername>`, o Policy Spy exportará a política desse computador, em vez do computador local.

> [!Note]  
> Essa opção de linha de comando não fornece uma maneira de especificar as credenciais do usuário. Para usar credenciais alternativas para acessar um computador remoto, use o comando **runas** para abrir um novo prompt de comando com as credenciais de segurança necessárias.  


## <a name="usage"></a>Uso

### <a name="tools-menu"></a>Menu Ferramentas

As seguintes ações estão disponíveis no menu **Ferramentas**:  

- **Abertura Remota**: conecta-se à política do cliente do Configuration Manager em um computador remoto. Use a caixa de diálogo Conectar para recuperar o nome do computador remoto e as credenciais de usuário opcionais. Se a conexão falhar, ela exibirá informações de erro no painel de Informações do Cliente. Se a conexão falhar novamente, tente conectar selecionando **Atualizar** no menu **Editar** ou pressionando F5.  

- **Abrir Arquivo**: abre um arquivo de exportação de política (XML) criado pela opção **Exportar Política**. A ferramenta exibe a política exportada exatamente como uma política em tempo real. Ela desabilita alguns recursos que se aplicam somente quando você se conecta a um cliente real.  

- **Solicitar Atribuições do Computador**: dispara uma solicitação de atribuições de política de computador no computador de destino. Esse recurso é desabilitado ao exibir uma política exportada.  

- **Avaliar Política do Computador**: dispara uma avaliação de política de computador no computador de destino. Este recurso está desabilitado ao exibir uma política exportada.  

- **Solicitar Atribuições de Usuário**: dispara uma solicitação de atribuições de política de usuário para o usuário conectado no momento. Esse recurso só está disponível ao exibir uma política no computador local.  

- **Avaliar Política de Usuário**: dispara uma avaliação de política de usuário para o usuário conectado no momento. Esse recurso só está disponível ao exibir uma política no computador local.  

- **Política de Redefinição**: remove todas as políticas não padrão e redefine os cookies de política para o site. Então dispara uma solicitação de computador para atribuições de política. Este recurso está desabilitado ao exibir uma política exportada.  

- **Exportar Política**: exporta a política do computador de destino para um arquivo XML. Exiba esse arquivo em qualquer computador com o Policy Spy. Para abrir o arquivo de exportação, selecione **Abrir Arquivo** no menu **Ferramentas**. Este recurso está desabilitado ao exibir uma política exportada.  


### <a name="edit-menu"></a>Menu Editar

As seguintes ações estão disponíveis no menu **Editar**:  

- **Excluir**: exclui a instância selecionada no painel Resultados. Essa ação tem suporte apenas para instâncias de política. Se você tentar excluir algo que não instâncias de política, a ferramenta exibirá uma mensagem de erro. Este recurso está desabilitado ao exibir uma política exportada.  

- **Atualizar**: atualiza todos os resultados para exibir as informações mais recentes. Todos os nós de árvore que são expandidos antes de atualizar são automaticamente expandidos depois. Se o Policy Spy não tive sido conectado com êxito à política do computador de destino, ele tentará se conectar novamente. Este recurso está desabilitado ao exibir uma política exportada.  

- **Limpar Eventos**: limpa todos os itens na guia Eventos.  



## <a name="results-pane"></a>Painel Resultados

O painel de resultados exibe as diferentes exibições do sistema de políticas no computador de destino. Acesse essas exibições clicando em uma das quatro guias a seguir: 
- [Real](#bkmk_policyspy-actual)
- [Solicitado](#bkmk_policyspy-requested)
- [Padrão](#bkmk_policyspy-default)
- [Eventos](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> Real

Essa guia exibe a atual política do cliente. A política atual determina o comportamento do cliente e o comportamento de seus agentes de cliente, como inventário e distribuição de software. A guia exibe os resultados em um formato de árvore com um nó raiz para o namespace do computador e cada namespace específico do usuário. Expanda um nó de namespace para exibir uma lista de classes. Expanda uma classe para exibir uma lista de suas instâncias. A lista de classe inclui somente as classes que têm instâncias.


### <a name="bkmk_policyspy-requested"></a> Solicitado

Essa guia exibe as atribuições de política que o cliente recuperou do seu site atribuído. A guia exibe os resultados em formato de árvore com um nó raiz para o namespace do Computador e cada namespace específico do usuário. Expandir um nó de namespace exibe os seguintes nós:  

- **Configuração**: exibe uma lista de classes de configuração derivadas de CCM_Policy_Config, que inclui o objeto de política, atribuições e outros.  

- **Configurações**: exibe todas as configurações ativas geradas por políticas. As configurações são exibidas sob o nó de configuração. 

> [!Note]   
> Pode haver várias instâncias com o mesmo nome porque o cliente ainda não mesclou essas configurações a conjunto resultante final. O Policy Spy exibe instâncias sob esse nó usando as propriedades de RealKey, em vez das suas chaves de política reais. Correlacione essas instâncias ao conjunto resultante exibido na guia real.  


### <a name="bkmk_policyspy-default"></a> Padrão

Essa guia exibe as mesmas informações que a guia **Solicitado**. Também inclui o conteúdo dos namespaces DefaultMachine e DefaultUser.


### <a name="bkmk_policyspy-events"></a> Eventos

Essa guia exibe os eventos do agente de política conforme eles ocorrem. A exibição cria uma assinatura de evento do WMI para todos os eventos derivados de CCM_PolicyAgent_Event. A exibição mostra um máximo de 200 eventos. Ela remove os eventos mais antigos da parte superior da lista conforme necessário. Se você selecionar o último item na lista, a lista rolará automaticamente para baixo enquanto adiciona novos eventos. Caso contrário, a exibição manterá sua posição atual e você deverá rolar para baixo ou pressionar a tecla End para exibir os novos eventos. Essa exibição está sempre vazia ao exibir uma política exportada.



## <a name="client-info-pane"></a>Painel de Informações do Cliente
O painel de Informações do Cliente exibe uma lista das propriedades do computador de destino. Ele exibirá as propriedades a seguir, se disponíveis:  
- Name
- ID
- Version
- Site
- MP atribuído
- MP residente
- MP do proxy
- Estado do proxy



## <a name="details-pane"></a>Painel de detalhes
O painel Detalhes exibe informações detalhadas sobre a seleção atual. Se nenhuma seleção estiver ativa, exibirá informações sobre o Policy Spy em si, incluindo a versão. Caso contrário, exibirá uma representação de MOF (Gerenciar Formato de Objeto) do item selecionado.

O Policy Spy usa a própria rotina de geração do MOF para criar uma exibição mais amigável do HTML que o MOF em texto sem formatação gerado pela WMI. Esse comportamento permite que o Policy Spy adicione os seguintes recursos para tornar o MOF mais legível:  

- Destaque de sintaxe  

- Matrizes e objetos recuados  

- As propriedades são organizadas em grupos locais, herdados e do sistema. Por padrão, recolhe os grupos de sistema e herdados. Você pode ver imediatamente quais propriedades a instância de fato usa.  

- Copie o MOF ou copie MOF em texto sem formatação para a área de transferência. Esse recurso é útil para colar o MOF em outros aplicativos chamando diretamente a ferramenta MofComp.  

Para instâncias de objetos de Política derivados de CCM_Policy_Policy, o painel de detalhes exibe o corpo da política abaixo do MOF que é exibido. Se o cliente não tiver baixado o corpo da política, o Policy Spy exibirá um hiperlink. Clique no link para baixar o corpo da política diretamente do ponto de gerenciamento do cliente. Se a ferramenta baixar com sucesso o corpo da política, ela substituirá o hiperlink pelo conteúdo da resposta. Caso contrário, o Policy Spy atualizará a exibição que indica que a solicitação falhou.

