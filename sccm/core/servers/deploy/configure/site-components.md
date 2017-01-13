---
title: Componentes do site | Microsoft Docs
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
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e22ffc898dc93f702f13417878aa6050d4cdd4ec


---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes do site para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Em cada site do System Center Configuration Manager, é possível configurar os componentes do site para modificar o comportamento de funções do sistema de sites e o relatório de status do site. Configurações de componente do site aplicam-se a um site e a cada instância de uma função de sistema de site aplicável no site.  

## <a name="about-site-components"></a>Sobre componentes do site  
 A maioria das opções para os vários componentes de site é autoexplicativa quando visualizada no console do Configuration Manager. No entanto, os detalhes a seguir podem ajudar a explicar algumas das configurações mais complexas ou direcioná-lo para conteúdo adicional que as explique:  

**Distribuição de software:**  

-   **Configurações de distribuição de conteúdo:**  você pode definir configurações que modificam o modo como o servidor do site transfere o conteúdo para seus pontos de distribuição. Quando você aumenta os valores usados para configurações de distribuição simultânea, a distribuição de conteúdo pode usar mais largura de banda de rede.  

-   **Conta de acesso à rede:** para obter informações sobre como configurar e usar a conta de acesso à rede, consulte [Network Access Account (Conta de Acesso à Rede)](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)  

**Ponto de atualização de software:**  

-   Para obter informações sobre as opções de configuração para o componente do ponto de atualização de software, consulte [Install a software update point (Instalar um ponto de atualização de software)](../../../../sum/get-started/install-a-software-update-point.md).  

**Ponto de gerenciamento:**  

-   **Pontos de gerenciamento:** você pode configurar o site para publicar informações sobre seus pontos de gerenciamento nos Serviços de Domínio do Active Directory.  

     Os clientes do Configuration Manager usam os pontos de gerenciamento para localizar serviços, para encontrar informações do site como associação do grupo de limites e opções de seleção de certificado PKI e para encontrar outros pontos de gerenciamento no site e os pontos de distribuição dos quais o software pode ser baixado. Os clientes também usam pontos de gerenciamento para concluir a atribuição do site e baixar a política do cliente e carregar as informações do cliente.  

     Como o método mais seguro para localizar pontos de gerenciamento é publicá-los nos Serviços de Domínio Active Directory, geralmente, você sempre selecionará todos os pontos de gerenciamento em funcionamento para publicar nos Serviços de Domínio Active Directory. No entanto, esse método de local do serviço requer a extensão do esquema para o Configuration Manager; há um contêiner do **System Management** com permissões de segurança apropriadas para que o servidor do site publique nesse contêiner, que o site do esteja configurado para publicar no Active Directory Domain Services e que os clientes pertençam à mesma floresta do Active Directory que a floresta do servidor do site.  

     Quando os clientes na intranet não podem usar o Active Directory Domain Services para localizar pontos de gerenciamento, use a publicação [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

     Para obter informações gerais sobre o local do serviço, consulte [Understand how clients find site resources and services for System Center Configuration Manager (Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar pontos de gerenciamento de intranet selecionados no DNS:** especifique essa opção quando clientes na intranet não puderem localizar pontos de gerenciamento dos Serviços de Domínio do Active Directory, mas puderem usar um registro de recurso de local de serviço DNS (SRV RR) para localizar um ponto de gerenciamento em seu site atribuído.  

    Para o Configuration Manager publicar pontos de gerenciamento da intranet no DNS, todas as seguintes condições devem ser atendidas:  

    -   Os servidores DNS têm uma versão de BIND 8.1.2 ou posterior.  

    -   Servidores DNS são configurados para atualizações automáticas e dar suporte a registros de recurso de local do serviço.  

    -   Os FQDNs especificados para os pontos de gerenciamento no Configuration Manager têm entradas de host (registros A ou AAA) no DNS.  

    > [!WARNING]  
    >  Para os clientes localizarem pontos de gerenciamento publicados em DNS, atribua os clientes a um site específico (em vez de usar a atribuição automática de site) e configure-os para usarem o código de site com o sufixo do domínio do ponto de gerenciamento deles. Para obter informações, consulte [Locating Management Points (Localizando pontos de gerenciamento)](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

     Se os clientes do Configuration Manager não puderem usar o Active Directory Domain Services ou o DNS para localizar pontos de gerenciamento na intranet, eles retornarão ao uso de [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). O primeiro ponto de gerenciamento instalado para o site é automaticamente publicado para o WINS quando ele é configurado para aceitar conexões de cliente HTTP na intranet.  

**Relatório de status:**  

-   Essas configurações definem diretamente o nível de detalhes incluído nos relatórios de status de sites e clientes.  

**Notificação por email:**  

-   Especifique os detalhes de conta e do servidor de email para habilitar o Configuration Manager a enviar notificações por email para alertas.  

**Avaliação de associação da coleção:**  

-   Use essa tarefa para definir a frequência com que a associação da coleção é incrementalmente avaliada. A avaliação incremental atualiza uma associação de coleção apenas com recursos novos ou alterados.  

#### <a name="to-edit-the-site-components-at-a-site"></a>Para editar os componentes do site em um site  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração de Site** > **Sites** e depois selecione o site que tem os componentes de site que você configurará.  

2.  Na guia **Início** , no grupo **Configurações** , clique em **Configurar Componentes do Site** e selecione o componente do site que você deseja configurar.  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Use o Configuration Manager Service Manager para gerenciar os componentes do site  
É possível usar o Configuration Manager Service Manager para controlar os serviços do Configuration Manager e exibir o status de qualquer serviço do Configuration Manager ou o thread de trabalho (chamados coletivamente de componentes do Configuration Manager):  

-   Os componentes do Configuration Manager podem ser executados em qualquer sistema de sites.  

-   Os componentes são gerenciados da mesma forma como você gerencia serviços no Windows. é possível iniciar, parar, pausar, retomar ou consultar componentes do Configuration Manager.  

O serviço do Configuration Manager é executado quando há algo para ele fazer (geralmente, quando um arquivo de configuração é gravado na caixa de entrada de algum componente). Se você precisar identificar o componente envolvido em uma operação, será possível usar o **Configuration Manager Service Manager** para manipular vários serviços e threads do Configuration Manager e depois exibir a alteração resultante no comportamento do Configuration Manager. Por exemplo, é possível parar os serviços do Configuration Manager, um de cada vez, até que determinada resposta seja eliminada. Isso permite que você determine qual serviço causa o comportamento.  

> [!TIP]  
>  O procedimento a seguir pode ser usado para manipular a operação dos componentes do Configuration Manager.  

#### <a name="to-use-the-configuration-manager-service-manager"></a>Para usar o Configuration Manager Service Manager  

1.  No console do Configuration Manager, clique em **Monitoramento** >  **Status do Sistema** e depois clique em **Status do componente**.  

2.  Na guia **Início** , no grupo **Componente** , clique em **Iniciar**e selecione **Configuration Manager Service Manager**.  

3.  Quando o Configuration Manager Service Manager abrir, conecte-se ao site que deseja gerenciar.  

     Se você não vir o site que deseja gerenciar, clique em **Site**, clique em **Conectar**e insira o nome do servidor do site correto.  

4.  Expanda o site e navegue até **Componentes** ou **Servidores** , dependendo de onde estejam localizados os componentes que você quer gerenciar.  

5.  No painel direito, selecione um ou mais componentes e, no menu **Componente** , clique em **Consultar** para atualizar o status da sua seleção.  

6.  Atualizado o status do componente, use uma das quatro opções com base em ações no menu **Componente** para modificar a operação dos componentes. Depois de solicitar uma ação, você deverá consultar o componente para exibir o novo status dele.  

7.  Feche o Configuration Manager Service Manager depois de concluir a modificação do status operacional dos componentes.  



<!--HONumber=Dec16_HO3-->


