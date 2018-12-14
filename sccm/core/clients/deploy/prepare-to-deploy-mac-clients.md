---
title: Preparar para implantar o cliente em Macs
titleSuffix: Configuration Manager
description: As tarefas de configuração antes da implantação do cliente do Configuration Manager em Macs.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7fc0a7ca3dd6974d1c97445d69b8f6032e81835
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455896"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparar para implantar o software cliente em Macs

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Siga estas etapas para estar pronto para [implantar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).



## <a name="mac-prerequisites"></a>Pré-requisitos do Mac

O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. Baixe os **Clientes para sistemas operacionais adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

Para obter a lista de versões com suporte, confira [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers).



## <a name="certificate-requirements"></a>Requisitos de certificado

A instalação e o gerenciamento do cliente para computadores Mac exigem certificados de PKI (infraestrutura de chave pública). Os certificados PKI protegem a comunicação entre os computadores Mac e o site do Configuration Manager usando autenticação mútua e transferência de dados criptografados. O Configuration Manager pode solicitar e instalar um certificado de cliente do usuário. Ele usa os serviços de certificados com uma autoridade de certificação corporativa e o ponto de registro do Configuration Manager e o ponto proxy do registro. Você também pode solicitar e instalar um certificado de computador independentemente do Configuration Manager. Esse certificado deve atender aos requisitos de certificado do Configuration Manager.  

Os clientes Mac do Configuration Manager sempre verificam revogação de certificados. Não é possível desabilitar essa função.  

Se os clientes Mac não puderem localizar a CRL (lista de certificados revogados), eles não poderão se conectar a sistemas de sites do Configuration Manager. Especialmente para os clientes Mac em uma floresta diferente para a autoridade de certificação emissora, verifique o design da sua CRL. Garanta que os clientes Mac possam localizar e baixar uma CRL.  

Antes de instalar o cliente do Configuration Manager em um computador Mac, decida como o certificado do cliente será instalado:  

-   Usar o registro do Configuration Manager usando a [ferramenta CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de registro não dá suporte para a renovação automática de certificados. Registre novamente os computadores Mac antes da expiração do certificado.  

-   [Usar um método de solicitação e de instalação de certificado independente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Para obter mais informações sobre os requisitos de certificado de cliente Mac, confira [Requisitos de certificado PKI para o Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

Os clientes Mac são atribuídos automaticamente ao site do Configuration Manager que os gerencia. Os clientes Mac serão instalados como clientes somente de Internet, mesmo se a comunicação for restrita à intranet. Essa configuração significa que eles se comunicam com pontos de gerenciamento habilitados para Internet e pontos de distribuição em seu site atribuído. Os computadores Mac não se comunicam com sistemas de site fora do site atribuído.  

> [!IMPORTANT]  
>  O cliente do Configuration Manager para macOS não pode ser usado para se conectar a um ponto de gerenciamento configurado para usar uma [réplica de banco de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implantar um certificado do servidor Web nos servidores do sistema de sites  

Caso os sistemas de sites ainda não tenham um certificado do servidor Web, implante um nos computadores que têm as funções de sistema de sites a seguir:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

-   Ponto de registro  

-   Ponto proxy do registro  

O Certificado do servidor Web deve incluir o FQDN de Internet especificado nas propriedades de sistema de site. O servidor não precisa ser acessível pela Internet para dar suporte a computadores Mac. Se você não precisa de gerenciamento de clientes baseado na Internet, pode especificar o valor de FQDN de intranet para o FQDN de Internet.  

Especifique o valor do FQDN de Internet do sistema de sites no certificado do servidor Web para o ponto de gerenciamento, o ponto de distribuição e o ponto proxy do registro.

Para obter mais informações de um exemplo de implantação, confira [Implantando o certificado do servidor Web para sistemas de sites que executam o IIS](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implantar um certificado de autenticação de cliente nos servidores do sistema de sites  

Caso os sistemas de sites ainda não tenham um certificado de autenticação de cliente, implante um nos computadores que hospedam as funções de sistema de sites a seguir:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de gerenciamento, confira [Implantando o certificado do cliente para computadores com Windows](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de distribuição, confira [Implantando o certificado do cliente para pontos de distribuição](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Para implantar o cliente em dispositivos que executam o macOS Sierra, o nome da entidade do certificado do ponto de gerenciamento deve estar configurado corretamente. Por exemplo, use o FQDN do servidor do ponto de gerenciamento.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar o modelo de certificado do cliente para Macs  

O modelo de certificado deve ter permissões de **Leitura** e **Registro** para a conta de usuário que registra o certificado no computador Mac.  

Para obter mais informações, confira [Implantando o certificado do cliente em computadores Mac](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configurar o ponto de gerenciamento e o ponto de distribuição  

Configure os pontos de gerenciamento para as seguintes opções:  

-   HTTPS  

-   Permitir conexões do cliente por meio da Internet. Esse valor de configuração é necessário para gerenciar computadores Mac. No entanto, isso não significa que os servidores do sistema de site devem ser acessíveis pela Internet.  

-   Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento  

Pontos de distribuição não são necessários para instalar o cliente para Mac. Se você quiser implantar software nesses computadores depois de instalar o cliente, configure pontos de distribuição para permitir conexões de cliente da Internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gerenciamento e pontos de distribuição para dar suporte a Mac  

Antes de iniciar este procedimento, configure o ponto de gerenciamento e o ponto de distribuição com um FQDN de Internet. Se esses servidores não derem suporte ao gerenciamento de clientes baseado na Internet, você poderá especificar o FQDN de intranet como o valor de FQDN de Internet.

As funções de sistema de sites devem estar em um site primário.  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Funções do Sistema de Sites e Servidores**. Em seguida, selecione o servidor que tem as funções do sistema de site corretas.  

2.  No painel de detalhes, selecione a função **Ponto de gerenciamento** e, em seguida, selecione **Propriedades** na faixa de opções. Na janela **Propriedades do ponto de gerenciamento**, configure estas opções:  

    1.  Escolha **HTTPS**.  

    2.  Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    3.  Escolha **Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento**.  

    4. Selecione **OK** para salvar esta configuração.  

3.  No painel de detalhes do nó de servidor e Funções do Sistema do Site, selecione a função **Ponto de Distribuição** e selecione **Propriedades** na faixa de opções. Na janela **Propriedades do ponto de distribuição**, configure estas opções:  

    -   Escolha **HTTPS**.  

    -   Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    -   Escolha **Importar certificado**, navegue até o arquivo do certificado do ponto de distribuição do cliente exportado e especifique a senha.  

4.  Repita este procedimento para todos os pontos de gerenciamento e pontos de distribuição em sites primários que gerenciam computadores Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar o ponto proxy do registro e o ponto de registro  

Instale ambas as funções no mesmo site. Não é necessário instalá-las no mesmo servidor do sistema de site ou na mesma floresta do Active Directory.  

Para obter mais informações sobre as considerações e o posicionamento da função do sistema de sites, confira [Funções do sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles#bkmk_planroles).  

Estes procedimentos configuram as funções do sistema de site para oferecer suporte a computadores Mac:   

-   [Novo servidor do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles#to-install-site-system-roles-on-a-new-site-system-server)  

-   [Servidor do sistema de sites existente](/sccm/core/servers/deploy/configure/install-site-system-roles#bkmk_Install)    

Em qualquer caso, na página **Seleção de Função do Sistema**, selecione **Ponto proxy do registro** e **Ponto de registro** na lista de funções disponíveis.  



## <a name="install-the-reporting-services-point"></a>Instale o ponto do Reporting Services  

Para obter mais informações, confira [Instalar o ponto do Reporting Services](/sccm/core/servers/manage/configuring-reporting).  



## <a name="next-steps"></a>Próximas etapas

[Implantar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  
