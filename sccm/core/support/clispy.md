---
title: Client Spy
titleSuffix: Configuration Manager
description: Use o Client Spy para solucionar problemas de distribuição de software, inventário e medição de software em clientes do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e798c11bbbd6c6d69ea8455ecb7b0252a408659d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385927"
---
# <a name="client-spy"></a>Client Spy

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Client Spy é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). É uma ferramenta para solucionar problemas de distribuição de software, inventário e medição de software em clientes do Configuration Manager. 

A maioria das informações recuperadas pela ferramenta se refere às implantações de software:
- Todas as implantações de software atuais 
- Histórico de distribuição de software
- A configuração de cache do cliente
- Itens em cache
- Implantações necessárias pendentes
- Implantações disponíveis  

Também exibe as seguintes informações de inventário
- A data do último ciclo de inventário
- A data do último relatório
- Versões principais e secundárias do inventário de software
- Coleta de arquivos
- Inventário de hardware
- Coleta de IDMIF
- DDRs (registro dos dados de descoberta) 

As regras de medição de software também são exibidas. 

> [!Note]   
> Para melhorar o desempenho, a ferramenta coleta informações para cada guia quando você a seleciona. Da mesma forma, quando você clica em **Atualizar**, ela só atualiza as informações na guia exibida no momento.



## <a name="usage"></a>Uso


### <a name="tools-menu"></a>Menu Ferramentas

As seguintes ações estão disponíveis no menu **Ferramentas**:  

#### <a name="connect"></a>Connect
Recupere informações de um computador diferente.  

- Por padrão, a ferramenta exibe informações do computador atual. 

- Conecte-se usando o nome do computador remoto, o nome de usuário e a senha da conta. A ferramenta faz uma conexão ao compartilhamento IPC$ no computador remoto. Ela exclui a conexão quando a ferramenta é encerrada ou quando você se conectar a outro computador.  

- Ela requer uma conta com credenciais suficientes para obter as informações.  

- Se você não especificar um nome de usuário e senha, o Client Spy usará o contexto de segurança do usuário conectado no momento para tentar estabelecer a conexão.  

- Quando você se conecta a um computador remoto, todas as guias exibidas mostram informações do computador remoto.

#### <a name="software-distribution"></a>Distribuição de software
Exibe as guias [Distribuição de Software](#software-distribution) e oculta as outras guias. Por padrão, o Client Spy exibe as guias de Distribuição de Software.

#### <a name="inventory"></a>Inventário
Exibe a guia de Inventário e oculta as outras guias.

#### <a name="software-metering"></a>Medição de software
Exibe a guia de Medição de Software e oculta as outras guias.

#### <a name="save-current-tab-to-file"></a>Salvar guia atual em arquivo
Salva as informações na guia exibida no momento em um arquivo de texto que você especifica. 

#### <a name="save-all-tabs-to-file"></a>Salvar todas as guias em um arquivo
Salva as informações em todas as guias em um arquivo de texto que você especifica. Somente salva informações que sua conta pode ver.



## <a name="software-distribution-tab"></a>Guia Distribuição de Software

Defina as configurações nas quatro guias a seguir:
- [Solicitações de Execução de Distribuição de Software](#bkmk_exec-requests)
- [Histórico de Distribuição de Software](#bkmk_history)
- [Informações de Cache de Distribuição de Software](#bkmk_cache-info)
- [Execuções Pendentes de Distribuição de Software](#bkmk_pending-exec)


### <a name="bkmk_exec-requests"></a> Solicitações de Execução de Distribuição de Software

Essa guia exibe todas as implantações existentes, incluindo implantações em dispositivo e direcionadas ao usuário.

Cada item de árvore na guia Solicitações de Execução de Distribuição de Software contém os quatro atributos a seguir:
- ID do anúncio. Esse valor poderá ficar em branco se for uma implantação disponível. 
- ID do Pacote 
- Nome do Programa 
- Usuário. Pode ser SID Do usuário de destino ou SID do usuário que iniciou a solicitação. Se ambas forem solicitações do sistema, o usuário exibido será Sistema. 

Para cada solicitação de execução, também são exibidas as seguintes informações em uma estrutura de subárvore:
- Nome do Programa 
- ID do Pacote 
- Nome do pacote 
- Hora de Criação da Solicitação 
- Estado 
- Estado de Execução, se o estado for Execução 
- Contexto de Execução (Usuário ou Administrador) 
- Estado do Histórico (Success, Failure ou NotRun) 
- LastRunTime (Nunca, se o programa não tiver sido executado antes) 
- RetryCount, se o Estado for WaitingRetry 
- ContentAccess (Contagem de Repetições, se Estado for WaitingRetry) 
- FailureCode, se o estado for WaitingRetry 
- FailureReason, se o Estado for WaitingRetry 

Se a solicitação exigir o conteúdo, o estado será WaitingContent. A guia Informações do Cache de Distribuição de Software mostra os detalhes para essa solicitação de download.

Se a solicitação de execução for uma solicitação de download, ela também exibirá o número de bytes baixados.

> [!Note]   
> Ela usa ícones diferentes para vários estados de uma solicitação de execução.


### <a name="bkmk_history"></a> Histórico de Distribuição de Software

Essa guia contém informações sobre todos os programas executados anteriormente. Essas informações são armazenadas no Registro.

Os branches principais dessa árvore são os diferentes históricos do usuário, incluindo o Sistema. É exibida uma subárvore contendo a lista de pacotes dos quais os programas foram executados para cada usuário. 

O nome do pacote e a ID do pacote para cada subárvore do pacote exibe uma lista de programas que foram executados. Exibe os seguintes atributos para cada: 
- Nome do programa
- Estado de execução
- Hora da última execução
- Código de falha
- Razão da falha  

O código de falha e o motivo da falha ficam em branco quando um programa foi executado com êxito.


### <a name="bkmk_cache-info"></a> Informações de Cache de Distribuição de Software

#### <a name="cache-config"></a>Config de Cache
Contém informações sobre o cache de Cliente do Configuration Manager. Essas informações incluem o local do cache, o tamanho do cache e se ele está atualmente em uso. 

#### <a name="cached-items"></a>Itens em cache
Contém uma subárvore de todos os itens atualmente no cache. Cada item da árvore inclui as seguintes informações sobre cada item: 
- O local do item (pasta) no cache
- Estado atual
- ID do Pacote
- Nome do pacote
- Versão do pacote
- Tamanho do pacote
- Contagem de referência atual
- Hora da última referência (UTC)  

#### <a name="downloading-items"></a>Baixando Itens
São os itens que o cliente está baixando no momento. Cada um deles mostra as mesmas informações exibidas pelos itens em cache e o número de quilobytes baixado. 


### <a name="bkmk_pending-exec"></a> Execuções Pendentes de Distribuição de Software

Esta guia contém informações que detalham implantações passadas e futuras necessárias e uma lista de implantações disponíveis.

Cada ramificação da árvore é para cada conta de usuário com as implantações disponíveis, incluindo o Sistema.

Para cada usuário, uma subárvore contém os três itens a seguir:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Anúncios Obrigatórios com Execuções Futuras
Esses são anúncios obrigatórios que ainda têm programas restantes para serem executados. Eles podem ser anúncios de agendamento recorrente, único ou múltiplo. Cada um exibe a ID de anúncio, a hora da próxima execução e o agendamento no qual o anúncio é executado. 

#### <a name="optional-advertisements"></a>Anúncios Opcionais
Exibe uma lista de todos os anúncios publicados. Também exibe detalhes, como a ID de anúncio, nome do programa e nome do pacote para cada um. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Anúncios obrigatórios passados sem execuções agendadas futuras
Esta é uma lista de anúncios que existem no cliente que não têm programas futuros agendados para execução. A ID de anúncio, o nome do pacote e o nome do programa são exibidos. Um item de subárvore é exibido para todos os anúncios opcionais.

> [!Note]  
> Informações de nome de pacote só estão disponíveis para pacotes que anunciaram políticas associadas a eles no computador que está sendo visualizado. Pacotes que não têm mais políticas disponíveis associadas a eles exibem a mensagem "Nome do Pacote Não está mais Disponível".  



## <a name="inventory-tab"></a>Guia de Inventário

Há apenas uma guia contendo informações de inventário. A árvore principal contém os cinco itens a seguir:  

- **Inventário de Software**: contém a data em que o último ciclo foi iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Coleta de Arquivos**: contém a data em que o último ciclo foi iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Inventário de Hardware**: contém a data em que o último ciclo foi iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **Coleta de IDMIF**: contém a data em que o último ciclo foi iniciado, a data do último relatório e as versões principais e secundárias do último relatório.  

- **DDR**: contém a data em que o último ciclo foi iniciado, a data do último relatório e as versões principais e secundárias do último relatório. As informações de DDR também são exibidas em uma subárvore.



## <a name="software-metering-tab"></a>Guia Medição de Software

Essa guia exibe informações como uma subárvore e inclui todas as regras de medição de software. Ela exibe cada regra como um nó, que identifica pelo nome de arquivo e pela ID da regra. Expanda cada nó na árvore e exiba as seguintes informações:
- Nome do arquivo do Explorer 
- Nome do arquivo original
- ID da Regra
- Versão do arquivo
- Linguagem


