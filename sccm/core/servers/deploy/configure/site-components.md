---
title: Componentes do site do Configuration Manager | Microsoft Docs
description: "Saiba como configurar os componentes do site para modificar o comportamento de funções do sistema de sites e o relatório de status do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Em cada site do System Center Configuration Manager, é possível configurar os componentes do site para modificar o comportamento de funções do sistema de sites e o relatório de status do site. As configurações de componente do site aplicam-se a um site e a cada instância de uma função do sistema de sites aplicável no site.  

## <a name="about-site-components"></a>Sobre componentes do site  
 A maioria das opções para os vários componentes de site é autoexplicativa quando visualizada no console do Configuration Manager. No entanto, os detalhes a seguir podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para conteúdo adicional que as explique.  

### <a name="software-distribution"></a>Distribuição de software  

-   **Configurações de distribuição de conteúdo:** você pode especificar configurações que modificam o modo como o servidor do site transfere o conteúdo para seus pontos de distribuição. Quando você aumenta os valores usados para configurações de distribuição simultânea, a distribuição de conteúdo pode usar mais largura de banda de rede.  

-   **Conta de acesso à rede:** para obter informações sobre como configurar e usar a conta de acesso à rede, consulte [Conta de Acesso à Rede](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Ponto de atualização de software  

-   Para obter informações sobre as opções de configuração para o componente do ponto de atualização de software, consulte [Instalar um ponto de atualização de software](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Ponto de gerenciamento  

-   **Pontos de gerenciamento:** você pode configurar o site para publicar informações sobre seus pontos de gerenciamento no Active Directory Domain Services.  

     Os clientes do Configuration Manager usam pontos de gerenciamento para localizar serviços e para encontrar informações do site, como associação do grupo de limites e as opções de seleção de certificado PKI. Os clientes também usam pontos de gerenciamento para localizar outros pontos de gerenciamento no site, bem como pontos de distribuição dos quais é possível baixar o software. Os pontos de gerenciamento também ajudam os clientes a concluir a atribuição de site e baixar a política do cliente e carregar as informações do cliente.  

     Como o método mais seguro para localizar pontos de gerenciamento é publicá-los nos Serviços de Domínio Active Directory, geralmente, você sempre selecionará todos os pontos de gerenciamento em funcionamento para publicar nos Serviços de Domínio Active Directory. No entanto, esse método de localização de serviço exige que o seguinte seja verdadeiro:

     - O esquema é estendido para o Configuration Manager.
     - Há um contêiner **Gerenciamento do Sistema**, com permissões de segurança apropriadas para o servidor do site para publicar nesse contêiner.
     - O site do Configuration Manager é configurado para publicar no Active Directory Domain Services.
     - Os clientes pertencem à mesma floresta do Active Directory que a floresta do servidor do site.  

     Quando os clientes na intranet não podem usar o Active Directory Domain Services para localizar pontos de gerenciamento, use a publicação [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

 Para obter informações gerais sobre o local do serviço, consulte [Understand how clients find site resources and services for System Center Configuration Manager (Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar pontos de gerenciamento selecionados da intranet em DNS:** especifique essa opção quando os clientes na intranet não conseguem localizar os pontos de gerenciamento do Active Directory Domain Services. Em vez disso, eles podem usar um registro de recurso de local do serviço (SRV RR) DNS para localizar um ponto de gerenciamento em seu site atribuído.  

    Para o Configuration Manager publicar pontos de gerenciamento da intranet no DNS, todas as seguintes condições devem ser atendidas:  

    -   Os servidores DNS têm uma versão de BIND 8.1.2 ou posterior.  

    -   Servidores DNS são configurados para atualizações automáticas e dar suporte a registros de recurso de local do serviço.  

    -   Os FQDNs (nomes de domínio totalmente qualificados) especificados para os pontos de gerenciamento no Configuration Manager têm entradas de host (registros A ou AAA) no DNS.  

    > [!WARNING]  
    >  Para os clientes encontrarem pontos de gerenciamento publicados no DNS, você deve atribuir os clientes a um site específico (em vez de usar a atribuição de site automática). Configure esses clientes para usar o código do site com o sufixo de domínio de seu ponto de gerenciamento. Para obter informações, consulte [Localizando pontos de gerenciamento](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) em [Como atribuir clientes a um site no System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Se os clientes do Configuration Manager não puderem usar o Active Directory Domain Services ou o DNS para localizar pontos de gerenciamento na intranet, eles usarão o [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). O primeiro ponto de gerenciamento instalado para o site é automaticamente publicado para o WINS quando ele é configurado para aceitar conexões de cliente HTTP na intranet.  

### <a name="status-reporting"></a>Relatório de status  

-   Essas configurações definem diretamente o nível de detalhes incluído nos relatórios de status de sites e clientes.  

### <a name="email-notification"></a>Notificação por email  

-   Especifique os detalhes de conta e do servidor de email para habilitar o Configuration Manager a enviar notificações por email para alertas.  

### <a name="collection-membership-evaluation"></a>Avaliação de associação da coleção  

-   Use essa tarefa para definir a frequência com que a associação da coleção é incrementalmente avaliada. A avaliação incremental atualiza uma associação de coleção apenas com recursos novos ou alterados.  

### <a name="edit-the-site-components-at-a-site"></a>Para editar os componentes do site em um site  

Use as etapas a seguir para editar os componentes do site:

1.  No console do Configuration Manager, clique em **Administração** > **Configuração de Site** > **Sites** e depois selecione o site que tem os componentes de site que você deseja configurar.  

2.  Na guia **Início**, no grupo **Configurações**, clique em **Configurar Componentes do Site**. Em seguida, selecione o componente do site que deseja configurar.  

##  <a name="BKMK_ServiceMgr"></a> Use o Configuration Manager Service Manager para gerenciar os componentes do site  
É possível usar o Configuration Manager Service Manager para controlar os serviços do Configuration Manager e exibir o status de qualquer serviço do Configuration Manager ou o thread de trabalho (chamados coletivamente de componentes do Configuration Manager). Compreenda o seguinte sobre componentes do Configuration Manager:  

-   Os componentes podem ser executados em qualquer sistema de sites.  

-   Os componentes são gerenciados da mesma maneira que você gerencia os serviços no Windows. Você pode iniciar, parar, pausar, retomar ou consultar componentes do Configuration Manager.  

O serviço do Configuration Manager é executado quando há algo para ele fazer (geralmente, quando um arquivo de configuração é gravado na caixa de entrada de algum componente). Se for necessário identificar o componente envolvido em uma operação, você poderá usar o Configuration Manager Service Manager para manipular vários serviços e threads. Você pode então exibir a alteração resultante no comportamento do Configuration Manager. Por exemplo, é possível parar os serviços do Configuration Manager, um de cada vez, até que determinada resposta seja eliminada. Isso permite que você determine qual serviço causa o comportamento.  

> [!TIP]  
>  O procedimento a seguir pode ser usado para manipular a operação dos componentes do Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Usar o Configuration Manager Service Manager  

1.  No console do Configuration Manager, clique em **Monitoramento** >  **Status do Sistema** e depois clique em **Status do componente**.  

2.  Na guia **Início**, no grupo **Componente**, clique em **Iniciar**. Em seguida, selecione **Configuration Manager Service Manager**.  

3.  Quando o Configuration Manager Service Manager abrir, conecte-se ao site que deseja gerenciar.  

     Se você não vir o site que deseja gerenciar, clique em **Site**, clique em **Conectar**e insira o nome do servidor do site correto.  

4.  Expanda o site e navegue até **Componentes** ou **Servidores**, dependendo de onde estejam localizados os componentes que você quer gerenciar.  

5.  No painel direito, selecione um ou mais componentes. Em seguida, no menu **Componente**, clique em **Consultar** para atualizar o status da seleção.  

6.  Atualizado o status do componente, use uma das quatro opções com base em ações no menu **Componente** para modificar a operação dos componentes. Depois de solicitar uma ação, você deverá consultar o componente para exibir o novo status dele.  

7.  Feche o Configuration Manager Service Manager depois de concluir a modificação do status operacional dos componentes.  

