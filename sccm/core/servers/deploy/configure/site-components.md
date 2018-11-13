---
title: Componentes do site
titleSuffix: Configuration Manager
description: Saiba como configurar os componentes do site para modificar o comportamento de funções do sistema de sites e o relatório de status do site.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ffe1a95252d575a5f828d46932f583f4276c5c0
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411167"
---
# <a name="site-components-for-configuration-manager"></a>Componentes do site para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para cada site do Configuration Manager, é possível configurar os componentes do site para modificar o comportamento de funções do sistema de sites e o relatório de status do site. As configurações de componente do site aplicam-se a um site e a cada instância de uma função do sistema de sites aplicável no site.  

No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione um site. No grupo **Configurações** da faixa de opções, clique em **Configurar componentes do site**. Selecione uma das seguintes opções:

- [Distribuição de software](#software-distribution)  
- [Ponto de atualização de software](#software-update-point)  
- [Ponto de gerenciamento](#management-point)  
- [Relatório de status](#status-reporting)  
- [Notificação por email](#email-notification)
- [Avaliação de associação da coleção](#bkmk_colleval)


## <a name="about-site-components"></a>Sobre componentes do site  

 A maioria das opções para os vários componentes de site é autoexplicativa quando visualizada no console do Configuration Manager. No entanto, os detalhes a seguir podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para conteúdo adicional.  

> [!Note]  
> As opções disponíveis para alguns componentes variam se você selecionar um site secundário, um site primário ou site de administração central. Alguns componentes não estão disponíveis em absoluto para determinados tipos de sites.  



### <a name="software-distribution"></a>Distribuição de software  

#### <a name="content-distribution-settings"></a>Configurações de distribuição de conteúdo
Na guia **Geral**, especifique as configurações que modificam o modo como o servidor do site transfere o conteúdo para seus pontos de distribuição. Quando você aumenta os valores usados para configurações de distribuição simultânea, a distribuição de conteúdo pode usar mais largura de banda de rede.  

#### <a name="pull-distribution-point"></a>Ponto de distribuição por pull
Para obter mais informações, consulte [Usar um ponto de distribuição pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

#### <a name="network-access-account"></a>Conta de acesso à rede
Para obter mais informações, confira [Conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="software-update-point"></a>Ponto de atualização de software  

Para mais informações, confira [Install a software update point](/sccm/sum/get-started/install-a-software-update-point) (Instalar um ponto de atualização de software).  


### <a name="management-point"></a>Ponto de gerenciamento  

Na guia **Geral**, configure o site para publicar informações sobre seus pontos de gerenciamento no Active Directory Domain Services.  

Os clientes do Configuration Manager usam pontos de gerenciamento para localizar serviços e para encontrar informações do site, como associação do grupo de limites e as opções de seleção de certificado PKI. Os clientes também usam pontos de gerenciamento para localizar outros pontos de gerenciamento no site, bem como pontos de distribuição dos quais é possível baixar o software. Os pontos de gerenciamento também ajudam os clientes a concluir a atribuição de site e baixar a política do cliente e carregar as informações do cliente.  

O método mais seguro para clientes localizarem pontos de gerenciamento na intranet é publicá-los no Active Directory Domain Services. Esse método de localização de serviço exige que o seguinte seja verdadeiro:

- O esquema é estendido para o Configuration Manager.
- Há um contêiner **Gerenciamento do Sistema**, com permissões de segurança apropriadas para o servidor do site para publicar nesse contêiner.
- O site do Configuration Manager é configurado para publicar no Active Directory Domain Services.
- Os clientes pertencem à mesma floresta do Active Directory que a floresta do servidor do site.  

Quando os clientes na intranet não podem usar o Active Directory Domain Services para localizar pontos de gerenciamento, use a [publicação DNS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns).  

Para obter informações gerais sobre a localização do serviço, confira [Entender como os clientes encontram serviços e recursos do site](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publicar pontos de gerenciamento selecionados da intranet em DNS
Especifique essa opção quando os clientes na intranet não podem localizar pontos de gerenciamento do Active Directory Domain Services. Em vez disso, eles podem usar um registro de recurso de local do serviço (SRV RR) DNS para localizar um ponto de gerenciamento em seu site atribuído.  

Para o Configuration Manager publicar pontos de gerenciamento da intranet no DNS, todas as seguintes condições devem ser atendidas:  

-   Os servidores DNS têm uma versão de BIND 8.1.2 ou posterior.  

-   Servidores DNS são configurados para atualizações automáticas e dar suporte a registros de recurso de local do serviço.  

-   Os FQDNs (nomes de domínio totalmente qualificados) especificados para os pontos de gerenciamento no Configuration Manager têm entradas de host (registros A ou AAA) no DNS.  

> [!WARNING]  
>  Para os clientes encontrarem pontos de gerenciamento publicados no DNS, você deve atribuir os clientes a um site específico (em vez de usar a atribuição de site automática). Configure esses clientes para usar o código do site com o sufixo de domínio de seu ponto de gerenciamento. Para obter mais informações, confira [Localizando pontos de gerenciamento](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).  

Se os clientes do Configuration Manager não puderem usar o Active Directory Domain Services ou o DNS para localizar pontos de gerenciamento na intranet, eles usarão o [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins). O primeiro ponto de gerenciamento instalado para o site é automaticamente publicado para o WINS quando ele é configurado para aceitar conexões de cliente HTTP na intranet.  


### <a name="status-reporting"></a>Relatório de status  

Essas configurações definem diretamente o nível de detalhes incluído nos relatórios de status de sites e clientes.  


### <a name="email-notification"></a>Notificação por email  

Especifique os detalhes de conta e do servidor de email para habilitar o Configuration Manager a enviar notificações por email para alertas.  

Para obter mais informações, veja [Usar alertas e o sistema de status](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="bkmk_colleval"></a> Avaliação de associação da coleção  

Use esse componente para definir a frequência com que a associação da coleção é incrementalmente avaliada. A avaliação incremental atualiza uma associação de coleção apenas com recursos novos ou alterados.  

Para obter mais informações, confira as [Práticas recomendadas para coleções](/sccm/core/clients/manage/collections/best-practices-for-collections).



##  <a name="BKMK_ServiceMgr"></a> Use o Configuration Manager Service Manager para gerenciar os componentes do site  

É possível usar o Configuration Manager Service Manager para controlar os serviços do Configuration Manager e exibir o status de qualquer serviço do Configuration Manager ou o thread de trabalho. Esses serviços e threads são chamados coletivamente de componentes do Configuration Manager. Compreenda as seguintes instruções sobre os componentes do Configuration Manager:  

-   Os componentes podem ser executados em qualquer sistema de sites.  

-   Os componentes são gerenciados da mesma maneira que você gerencia os serviços no Windows. Você pode iniciar, parar, pausar, retomar ou consultar componentes do Configuration Manager.  

Um serviço do Configuration Manager é executado quando há algo para ele fazer. Essa ação ocorre normalmente quando um arquivo de configuração é gravado na caixa de entrada do componente. 


### <a name="use-the-configuration-manager-service-manager"></a>Usar o Configuration Manager Service Manager  

1.  No console do Configuration Manager, vá até o workspace **Monitoramento**, expanda **Status do Sistema** e selecione o nó **Status do Componente**.  

2.  No grupo **Componente** da faixa de opções, selecione **Iniciar** e escolha **Configuration Manager Service Manager**.  

3.  Quando o Configuration Manager Service Manager abrir, conecte-se ao site que deseja gerenciar.  

     Se você não vir o site que deseja gerenciar, vá para o menu **Site** e selecione **Conectar**. Em seguida, insira o nome do servidor do site referente ao site correto.  

4.  Expanda o site e navegue até **Componentes** ou **Servidores**, dependendo de onde estejam localizados os componentes que você quer gerenciar.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, no menu **Componente**, selecione **Consultar** para atualizar o status da seleção.  

6.  Atualizado o status do componente, use uma das quatro opções com base em ações no menu **Componente** para modificar a operação dos componentes. Depois de solicitar uma ação, você deverá consultar o componente para exibir o novo status dele.  

7.  Feche o Configuration Manager Service Manager depois de concluir a modificação do status operacional dos componentes.  
