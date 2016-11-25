---
title: Sistema de sites para clientes | System Center Configuration Manager
description: "Determine funções do sistema de sites para clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 17f28ff5addfbfbab251bdb72be9b405487d1403


---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Adicionar as funções do sistema de sites para os clientes do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste artigo para ajudá-lo a determinar os sistemas de site de que você precisa para implantar clientes do Configuration Manager:  

 Para obter mais informações sobre onde instalar funções necessárias do sistema de sites na hierarquia, consulte [Design a hierarchy of sites for System Center Configuration Manager (Projetar uma hierarquia de sites para o System Center Configuration Manager)](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Para obter mais informações sobre como instalar e configurar as funções do sistema de sites de que você precisa, consulte [Install site system roles (Instalar funções do sistema de sites)](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="a-namebkmkdeterminempa-determine-whether-you-require-a-management-point"></a><a name="BKMK_Determine_MP"></a> Determinar se você precisa de um ponto de gerenciamento  
 Por padrão, todos os computadores cliente do Windows usarão um ponto de distribuição para instalar o cliente do Configuration Manager e poderão retornar a um ponto de gerenciamento quando não houver um ponto de distribuição disponível. No entanto, é possível instalar clientes do Windows em computadores de uma origem alternativa ao usar a propriedade de linha de comando CCMSetup **/source:<Caminho\>**. Por exemplo, isso poderá ser apropriado se você instalar clientes na Internet. Outro cenário é quando você quer evitar o envio de pacotes de rede entre o computador e o ponto de gerenciamento durante a instalação do cliente, talvez porque um firewall bloqueie as portas necessárias ao seu método de instalação ou você tenha uma conexão de baixa largura de banda. No entanto, todos os clientes devem se comunicar com um ponto de gerenciamento para serem atribuídos a um site e serem gerenciados pelo Configuration Manager.  

 Para obter mais informações sobre a propriedade da linha de comando do CCMSetup **/source:<Caminho\>**, consulte [About client installation properties in System Center Configuration Manager (Sobre as propriedades de instalação do cliente no System Center Configuration Manager)](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Quando você instala mais de um ponto de gerenciamento na hierarquia, os clientes se conectam automaticamente ao mais adequado, com base na sua associação na floresta e no local de rede. Não é possível instalar mais de um ponto de gerenciamento em um site secundário.  

 Os clientes de computadores Mac e clientes de dispositivos móveis registrados pelo Configuration Manager exigem sempre um ponto de gerenciamento para instalação do cliente. Esse ponto de gerenciamento deve estar em um site primário, deve ser configurado para oferecer suporte a dispositivos móveis e deve aceitar conexões de clientes da Internet. Esses clientes não podem usar pontos de gerenciamento em sites secundários nem se conectar a pontos de gerenciamento em outros sites primários.  

##  <a name="a-namebkmkdeterminefspa-determine-whether-you-require-a-fallback-status-point"></a><a name="BKMK_Determine_FSP"></a> Determinar se você precisa de um ponto de status de fallback  
 Você pode usar um ponto de status de fallback para monitorar a implementação do cliente em computadores Windows e identificar os clientes nesses computadores que não são gerenciados porque não podem se comunicar com um ponto de gerenciamento. Computadores Mac, dispositivos móveis registrados pelo Configuration Manager e dispositivos móveis gerenciados com o uso do conector do Exchange Server não usam ponto de status de fallback.  

> [!NOTE]  
>  Não é necessário ponto de status de fallback para monitorar a atividade e a integridade do cliente.  

 O ponto de status de fallback sempre se comunica com os clientes usando HTTP, que utiliza conexões não autenticadas e envia dados em texto não criptografado. Isso torna o ponto de status de fallback vulnerável a ataques, especialmente quando ele é usado no gerenciamento de cliente baseado na Internet. Para ajudar a reduzir a superfície sujeita a ataques, sempre dedique um servidor para executar o ponto de status de fallback e não instale outras funções do sistema de site no mesmo servidor em um ambiente de produção.  

 Instale um ponto de status de fallback se todas as seguintes condições se aplicarem:  

-   Você quer que os erros de comunicação do cliente de computadores Windows sejam enviados para o site, mesmo que esses computadores cliente não possam se comunicar com um ponto de gerenciamento.  

-   Use os relatórios de implantação do cliente do Configuration Manager, que exibem os dados enviados pelo ponto de status de fallback.  

-   Você tem um servidor dedicado para essa função do sistema de site e tem medidas adicionais de segurança para ajudar a proteger o servidor de ataques.  

-   Os benefícios de se usar um ponto de status de fallback superam todos os riscos de segurança associados a conexões não autenticadas e transferências de texto não criptografado pelo tráfego HTTP.  

 Não instale um ponto de status de fallback se a seguinte condição se aplicar:  

-   Os riscos de segurança ao se executar um site com conexões não autenticadas e transferências de texto não criptografado superam os benefícios da identificação de problemas de comunicação do cliente.  

##  <a name="a-namebkmkdeterminerspa-determine-whether-you-require-a-reporting-services-point"></a><a name="BKMK_Determine_RSP"></a> Determinar se você precisa de um ponto de serviços de relatório  
 O Configuration Manager fornece muitos relatórios para ajudar a monitorar a instalação, a atribuição e o gerenciamento de clientes no console do Configuration Manager. Alguns relatórios de implantação do cliente exigem que os clientes sejam atribuídos a um ponto de status de fallback.  

 Embora não seja obrigatório os relatórios implantarem clientes e seja possível ver algumas informações de implantação no console do Configuration Manager ou usar os arquivos de log do cliente para obter informações detalhadas, os relatórios do cliente fornecem informações valiosas para ajudar a monitorar e solucionar problemas de implantação de cliente.  

##  <a name="a-namebkmkdetermineenrollmentpointsa-determine-whether-you-require-an-enrollment-point-and-an-enrollment-proxy-point"></a><a name="BKMK_Determine_EnrollmentPoints"></a> Determinar se você precisa de um ponto de registro e de um ponto proxy do registro  
 O Configuration Manager requer o ponto de registro e o ponto proxy do registro para registrar dispositivos móveis e certificados para computadores Mac. Essas funções do sistema de sites não serão necessárias se você gerenciar dispositivos móveis usando o conector do Exchange Server, se instalar o cliente herdado do dispositivo móvel (por exemplo, para Windows CE) ou se solicitar e instalar o certificado de cliente em computadores Mac independentemente do Configuration Manager.  

##  <a name="a-namebkmkdeterminedpa-determine-whether-you-require-a-distribution-point"></a><a name="BKMK_Determine_DP"></a> Determinar se você precisa de um ponto de distribuição  
 Embora você não precise de um ponto de distribuição para instalar clientes do Configuration Manager em computadores Windows, por padrão, o Configuration Manager usa um ponto de distribuição para instalar os arquivos de origem do cliente em computadores com Windows, mas pode voltar a baixar esses arquivos por meio de um ponto de gerenciamento. Os pontos de distribuição não serão usados ​​para instalar clientes de dispositivos móveis registrados pelo Configuration Manager, mas serão usados ​​se você instalar o cliente herdado do dispositivo móvel. Se você instalar o cliente do Configuration Manager como parte de uma implantação de sistema operacional, a imagem do sistema operacional será armazenada e recuperada de um ponto de distribuição.  

 Embora você não precise de pontos de distribuição para instalar a maioria dos clientes do Configuration Manager, você precisará de pontos de distribuição para instalar softwares, tais como aplicativos e atualizações de software nos clientes.  

##  <a name="a-namebkmkdetermineapplicationcatalogpointsa-determine-whether-you-require-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a><a name="BKMK_Determine_ApplicationCatalogPoints"></a> Determinar se você precisa de um ponto de sites da Web do catálogo de aplicativos e de um ponto de serviços Web do catálogo de aplicativos  
 O ponto de site da Web do catálogo de aplicativos e o ponto de serviços da Web do catálogo de aplicativos não são necessários na implantação do cliente. No entanto, é possível instalá-los como parte do processo de implantação do cliente, para que os usuários possam executar as seguintes ações assim que o cliente do Configuration Manager for instalado nos computadores Windows:  

-   Apagar seus dispositivos móveis.  

-   Procurar e instalar aplicativos do catálogo de aplicativos.  

-   Implante aplicativos para usuários e dispositivos com a finalidade da implantação **Disponível**.  



<!--HONumber=Nov16_HO1-->


