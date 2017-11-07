---
title: "Configurar a segurança"
titleSuffix: Configuration Manager
description: "Configure as opções de segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 94699e41291b7e1c7072962595aa71384b03f27b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurar a segurança no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste artigo para ajudá-lo a configurar as opções relacionadas à segurança para o System Center Configuration Manager.  

##  <a name="BKMK_ConfigureClientPKI"></a> Definir configurações para certificados PKI de clientes  
Se você quiser usar certificados PKI (infraestrutura de chave pública) para conexões de clientes a sistemas de site que usam IIS (Serviços de Informações da Internet), use o procedimento a seguir para definir as configurações para esses certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para definir configurações de certificados PKI de clientes  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Configuração de Site**, escolha **Sites** e, em seguida, escolha o site primário a ser configurado.  

3.  Na guia **Início**, no grupo **Propriedades**, escolha **Propriedades** e, em seguida, escolha a guia **Comunicação de Computador Cliente**.  

    Essa guia está disponível somente em site primário. Se você não vir a guia **Comunicação de Computador Cliente** , verifique se você não está conectado a um site de administração central ou um site secundário.  

4.  Escolha **Somente HTTPS** quando quiser que os clientes atribuídos ao site sempre usem um certificado PKI de cliente ao se conectarem a sistemas de site que usam IIS. Ou escolha **HTTPS ou HTTP** quando você não exigir que os clientes usem certificados PKI.  

5.  Se você escolheu **HTTPS ou HTTP**, escolha **Usar certificado PKI de cliente (funcionalidade de autenticação de cliente) quando disponível** quando quiser usar um certificado PKI de cliente para conexões HTTP. O cliente usa esse certificado em vez de um certificado autoassinado para se autenticar para sistemas de site. Esta opção será escolhida automaticamente se você escolher **Somente HTTPS**.  

    Quando os clientes são detectados na Internet ou estão configurados para gerenciamento de cliente apenas de Internet, eles sempre usam um certificado PKI de cliente.  

6.  Escolha **Modificar** para configurar o método de seleção de cliente escolhido para quando houver mais de um certificado de cliente PKI válido disponível em um cliente e, em seguida, escolha **OK**.  

    Para saber mais sobre o método de seleção de certificado de cliente, consulte [Planejando a seleção de certificado PKI de cliente](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Marque ou desmarque a caixa de seleção para os clientes verificarem a CRL (lista de certificados revogados).  

    Para saber mais sobre a verificação de CRL para clientes, consulte [Planejando a revogação de certificado PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Se for necessário especificar certificados de autoridade de certificação (AC) raiz confiáveis para clientes, escolha **Definir**, importe os arquivos de certificado AC raiz e escolha **OK**.  

    Para saber mais sobre essa configuração, consulte [Planejando certificados PKI de Raiz Confiável e a Lista de emissores de certificados](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Escolha **OK** para fechar a caixa de diálogo de propriedades do site.  

Repita esse procedimento para todos os sites primários da hierarquia.  

##  <a name="BKMK_ConfigureSigningEncryption"></a> Configurar assinatura e criptografia  
Defina as configurações de assinatura e criptografia mais seguras para sistemas de site, às quais todos os clientes do site deem suporte. Essas configurações são especialmente importantes quando você permite que os clientes se comuniquem com sistemas de site usando certificados autoassinados por meio de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar assinatura e criptografia para um site  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Configuração de Site**, escolha **Sites** e, em seguida, escolha o site primário a ser configurado.  

3.  Na guia **Início**, no grupo **Propriedades**, escolha **Propriedades** e, em seguida, escolha a guia **Assinatura e Criptografia**.  

    Essa guia está disponível somente em site primário. Se você não vir a guia **Assinatura e Criptografia** , verifique se você não está conectado a um site de administração central ou um site secundário.  

4.  Configure as opções de assinatura e criptografia desejadas e escolha **OK**.  

    > [!WARNING]  
    >  Não escolha **Exigir SHA-256** sem antes verificar se todos os clientes que podem ser atribuídos ao site oferecem suporte a esse algoritmo de hash ou se eles têm um certificado de autenticação de cliente PKI válido. Talvez você precise instalar atualizações ou hotfixes nos clientes para dar suporte ao SHA-256. Por exemplo, computadores que executam Windows Server 2003 SP2 devem instalar um hotfix que é referido no [KB artigo 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Se você escolher essa opção e os clientes não oferecerem suporte ao SHA-256 e usarem certificados autoassinados, o Configuration Manager os rejeitará. Nesse cenário, o componente SMS_MP_CONTROL_MANAGER registra a identificação 5443 da mensagem.  

5.  Escolha **OK** para fechar a caixa de diálogo de **Propriedades** do site.  

Repita esse procedimento para todos os sites primários da hierarquia.  

##  <a name="BKMK_ConfigureRBA"></a> Configurar administração baseada em funções  
A administração baseada em funções combina funções de segurança, escopos de segurança e coleções atribuídas para definir o escopo administrativo para cada usuário administrativo. Um escopo administrativo inclui os objetos que um usuário administrativo pode exibir no console do Configuration Manager e as tarefas relacionadas a esses objetos que o usuário administrativo tem permissão para realizar. As configurações de administração baseada em funções são aplicadas em cada site de uma hierarquia.  

Os links a seguir destinam-se às seções relevantes do artigo [Configurar administração baseada em funções para o System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md):  

-   [Criar funções de segurança personalizadas](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurar escopos de segurança para um objeto](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerenciar a segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Criar um novo usuário administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modificar o escopo administrativo de um usuário administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Seu próprio escopo administrativo define os objetos e as configurações que você pode atribuir ao configurar a administração baseada em funções para outro usuário administrativo. Para obter informações sobre como planejar a administração baseada em funções, consulte [Fundamentos de administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="BKMK_ManageAccounts"></a> Gerenciar contas usadas pelo Configuration Manager  
O Configuration Manager dá suporte a contas do Windows para várias tarefas e usos diferentes.  

Use o procedimento a seguir para exibir as contas que estão configuradas para tarefas diferentes e para gerenciar a senha que o Configuration Manager usa para cada conta.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Para gerenciar contas usadas pelo Gerenciador de Configurações  

1.  No console do Configuration Manager, escolha **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Segurança** e, em seguida, escolha **Contas** para exibir as contas que estão configuradas para o Configuration Manager.  

3.  Para alterar a senha de uma conta que está configurada para o Configuration Manager, escolha a conta.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Escolha **Definir** para abrir a caixa de diálogo **Conta de Usuário do Windows** e especifique a nova senha para o Configuration Manager usar para a conta.  

    > [!NOTE]  
    >  A senha que você especificar deverá corresponder à senha especificada para a conta em Usuários e Computadores do Active Directory.  

6.  Escolha **OK** para concluir o procedimento.  
