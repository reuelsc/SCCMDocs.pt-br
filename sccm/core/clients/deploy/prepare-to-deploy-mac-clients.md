---
title: Preparar para implantar o software cliente em Macs | Microsoft Docs
description: "As tarefas de configuração antes da implantação do cliente do Configuration Manager em Macs."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 06dd4afe94c97b1ffd7d136666fddc623933fcd6
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparar para implantar o software cliente em Macs

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Siga estas etapas para assegurar que você está pronto para [implantar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs). 

## <a name="mac-prerequisites"></a>Pré-requisitos do Mac

O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. Baixe os **Clientes para Sistemas Operacionais Adicionais** no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Versões com suporte:**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra )  

## <a name="certificate-requirements"></a>Requisitos de certificado
A instalação e o gerenciamento do cliente para computadores Mac exigem certificados de PKI (infraestrutura de chave pública). Os certificados PKI protegem a comunicação entre os computadores Mac e o site do Configuration Manager usando autenticação mútua e transferência de dados criptografados. O Configuration Manager pode solicitar e instalar um certificado de cliente do usuário usando os Serviços de Certificados da Microsoft com uma AC (autoridade de certificação) corporativa e as funções do sistema de sites de ponto de registro e ponto proxy do registro do Configuration Manager. Ou você poderá solicitar e instalar um certificado de computador independentemente do Configuration Manager se o certificado atender aos requisitos do Configuration Manager.   
  
Os clientes Mac do Configuration Manager sempre executam a verificação de revogação de certificado. Não é possível desabilitar essa função.  
  
Se os clientes Mac não puderem confirmar o status de revogação de um certificado do servidor por não ter sido possível localizar a CRL, eles não poderão se conectar com êxito aos sistemas de sites do Configuration Manager. Especialmente para clientes Mac em uma floresta diferente da autoridade de certificação emissora, verifique o design da sua CRL para garantir que os clientes Mac possam localizar e se conectar a um CDP (ponto de distribuição) de CRL para estabelecer conexão com servidores do sistema de site.  

Antes de instalar o cliente do Configuration Manager em um computador Mac, decida como o certificado do cliente será instalado:  

-   Usar o registro do Configuration Manager usando a [ferramenta CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). O processo de registro não oferece suporte à renovação automática de certificados, portanto, é necessário registrar novamente os computadores Mac antes de o certificado instalado expirar.  

-   [Usar um método de solicitação e de instalação de certificado independente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Para obter mais informações sobre o requisito de certificado do cliente Mac e outros certificados PKI necessários para dar suporte a computadores Mac, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Os clientes Mac são atribuídos automaticamente ao site do Configuration Manager que os gerencia. Os clientes Mac são instalados como clientes somente de Internet, mesmo se a comunicação for restrita à intranet. Essa configuração de cliente significa que eles se comunicarão com as funções de sistema de site (pontos de gerenciamento e de distribuição) em seus sites atribuídos quando você configurar essas funções do sistema de site para permitir conexões de clientes por meio da Internet. Os computadores Mac não se comunicam com as funções do sistema de site fora do site atribuído.  

> [!IMPORTANT]  
>  O cliente Mac do Configuration Manager não pode ser usado para se conectar a um ponto de gerenciamento configurado para usar uma [réplica de banco de dados](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implantar um certificado do servidor Web nos servidores do sistema de sites  
Caso os sistemas de sites ainda não tenham um certificado do servidor Web, implante um nos computadores que têm as funções de sistema de sites a seguir:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

-   Ponto de registro  

-   Ponto proxy do registro  

O Certificado do servidor Web deve conter o FQDN de Internet especificado nas propriedades de sistema de site. O servidor não precisa ser acessível pela Internet para dar suporte a computadores Mac. Se você não precisa de gerenciamento de clientes baseado na Internet, pode especificar o valor de FQDN de intranet para o FQDN de Internet.  

Especifique o valor do FQDN de Internet do sistema de sites no certificado do servidor Web para o ponto de gerenciamento, o ponto de distribuição e o ponto proxy do registro. 

Para ver um exemplo de implantação que cria e instala esse certificado do servidor Web, consulte [Implantando o certificado do servidor Web para sistemas de sites que executam IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implantar um certificado de autenticação de cliente nos servidores do sistema de sites  
 Caso os sistemas de sites ainda não tenham um certificado de autenticação de cliente, implante um nos computadores que hospedam as funções de sistema de sites a seguir:  

-   Ponto de gerenciamento  

-   Ponto de distribuição  

 Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de gerenciamento, consulte [Implantando o certificado do cliente para computadores com Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 Para ver um exemplo de implantação que cria e instala o certificado do cliente para pontos de distribuição, consulte [Implantando o certificado do cliente para pontos de distribuição](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

>[!IMPORTANT]
>  Para implantar o cliente em dispositivos com macOS Sierra, o nome da entidade do certificado do ponto de gerenciamento deve estar configurado corretamente, por exemplo, usando o FQDN do servidor de ponto de gerenciamento.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar o modelo de certificado do cliente para Macs  

 O modelo de certificado deve ter permissões de **Leitura** e **Registro** para a conta de usuário que registrará o certificado no computador Mac.  

 Consulte [Implantando o certificado do cliente para computadores Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

## <a name="configure-the-management-point-and-distribution-point"></a>Configurar o ponto de gerenciamento e o ponto de distribuição  
 Configure os pontos de gerenciamento para as seguintes opções:  

-   HTTPS  

-   Permitir conexões do cliente por meio da Internet. Esse valor de configuração é necessário para gerenciar computadores Mac. No entanto, isso não significa que os servidores do sistema de site devem ser acessíveis pela Internet.  

-   Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento  

 Embora não sejam necessários pontos de distribuição para a instalação do cliente, você deverá configurar pontos de distribuição para permitir conexões de clientes por meio da Internet se desejar implantar software nesses computadores após o cliente ser instalado.  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar pontos de gerenciamento e pontos de distribuição para dar suporte a Mac  

Antes de iniciar esse procedimento, verifique se o servidor de sistema de site que executa o ponto de gerenciamento e o ponto de distribuição está configurado com um FQDN de Internet. Se esses servidores não derem suporte ao gerenciamento de clientes baseado na Internet, você poderá especificar o FQDN de intranet como o valor de FQDN de Internet. 

As funções de sistema de sites devem estar em um site primário.  


1.  No console do Configuration Manager, escolha **Administração** > **Configuração do Site** > **Funções de Servidores e Sistema de Site** e escolha o servidor com as funções do sistema de site corretas.  

3.  No painel de detalhes, clique com o botão direito do mouse no **Ponto de gerenciamento**, escolha **Propriedades de Função** e, na caixa de diálogo **Propriedades do Ponto de Gerenciamento**, configure as opções a seguir:  

    1.  Escolha **HTTPS**.  

    2.  Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    3.  Escolha **Permitir que dispositivos móveis e computadores Mac usem este ponto de gerenciamento**.  

4.  No painel de detalhes, clique com o botão direito do mouse em **Ponto de distribuição**, escolha **Propriedades de Função** e, na caixa de diálogo **Propriedades do Ponto de Distribuição**, configure as opções a seguir:  

    -   Escolha **HTTPS**.  

    -   Escolha **Permitir conexões de cliente apenas de Internet** ou **Permitir conexões de cliente de intranet e Internet**. Essas opções exigem um FQDN de Internet ou de intranet.  

    -   Escolha **Importar certificado**, navegue até o arquivo do certificado do ponto de distribuição do cliente exportado e especifique a senha.  

5.  Repita as etapas de 2 a 4 para todos os pontos de gerenciamento e de distribuição nos sites primários que você usará com Macs.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar o ponto proxy do registro e o ponto de registro  
 É necessário instalar ambas as funções de sistema de site no mesmo site, mas não é necessário instalá-las no mesmo servidor de sistema de site ou na mesma floresta do Active Directory.  

 Para obter mais informações e considerações sobre o posicionamento de funções de sistema de sites, consulte [Funções de sistema de sites](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) em [Planejar funções e servidores do sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Estes procedimentos configuram as funções do sistema de site para oferecer suporte a computadores Mac.   

-   [Novo servidor do sistema de sites](#new-site-system-server)  

-   [Servidor do sistema de sites existente](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>Novo servidor do sistema de site  

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração do Site** > **Funções de Servidores e Sistema de Site**  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Servidor do Sistema de Site**.  

4.  Na página **Geral**, especifique as configurações gerais do sistema de sites.  Não se esqueça de especificar um valor para o FQDN de Internet. Se o servidor não puder ser acessado pela Internet, use o FQDN de intranet.  

5.  Na página **Seleção de Função do Sistema**, selecione **Ponto proxy do registro** e **Ponto de registro** na lista de funções disponíveis.  

6.  Na página **Ponto Proxy do Registro**, examine as configurações e faça as alterações necessárias.  

7.  Na página **Configurações do Ponto de Registro**, examine as configurações e faça as alterações necessárias. Em seguida, conclua o assistente.  

### <a name="existing-site-system-server"></a>Servidor do sistema de site existente  

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração do Site** > **Funções de Servidores e Sistema de Site** e escolha o servidor que deseja usar para dar suporte a Macs.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Adicionar Funções do Sistema de Site**.  

4.  Na página **Geral** , especifique as configurações gerais para o sistema de site e clique em **Próximo**. Não se esqueça de especificar um valor para o FQDN de Internet. Se o servidor não puder ser acessado pela Internet, use o FQDN de intranet.   

5.  Na página **Seleção de Função do Sistema**, escolha **Ponto proxy do registro** e **Ponto de registro** na lista de funções disponíveis.  

6.  Na página **Ponto Proxy do Registro**, examine as configurações e faça as alterações necessárias.  

7.  Na página **Configurações do Ponto de Registro**, examine as configurações e faça as alterações necessárias. Em seguida, conclua o assistente.  

## <a name="install-the-reporting-services-point"></a>Instale o ponto do Reporting Services  
 [Instale o ponto do Reporting Services](../../../core/servers/manage/configuring-reporting.md) se você desejar executar relatórios para Macs.  

### <a name="next-steps"></a>Próximas etapas

[Implantar o cliente do Configuration Manager em computadores Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).  