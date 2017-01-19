---
title: "Configurar a segurança no System Center Configuration Manager | Microsoft Docs"
description: "Configure as opções de segurança no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: c486c196335174290a925ca59fe42b806d50889d


---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurar a segurança no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para ajudar a configurar as seguintes opções de segurança para o System Center Configuration Manager:  

-   [Configure Settings for Client PKI Certificates](#BKMK_ConfigureClientPKI)  

-   [Configurar assinatura e criptografia](#BKMK_ConfigureSigningEncryption)  

-   [Configure Role-Based Administration](#BKMK_ConfigureRBA)  

-   [Manage Accounts that are Used by Configuration Manager](#BKMK_ManageAccounts)  

##  <a name="a-namebkmkconfigureclientpkia-configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Definir configurações para certificados PKI de clientes  
Se você quiser usar certificados PKI (infraestrutura de chave pública) para conexões de clientes a sistemas de site que usam IIS (Serviços de Informações da Internet), use o procedimento a seguir para definir as configurações para esses certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para definir configurações de certificados PKI de clientes  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**, clique em **Sites**e depois no site primário a ser configurado.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**e clique na guia **Comunicação de Computador Cliente** .  

    Essa guia está disponível somente em site primário. Se você não vir a guia **Comunicação de Computador Cliente** , verifique se você não está conectado a um site de administração central ou um site secundário.  

4.  Clique em **Somente HTTPS** quando quiser que os clientes atribuídos ao site sempre usem um certificado PKI de cliente ao se conectarem a sistemas de site que usam IIS. Ou clique em **HTTPS ou HTTP** quando você não exigir que os clientes usem certificados PKI.  

5.  Se você tiver selecionado **HTTPS ou HTTP**, clique em **Usar certificado PKI de cliente (recurso de autenticação de cliente) quando disponível** quando quiser usar um certificado PKI de cliente para conexões HTTP. O cliente usa esse certificado em vez de um certificado autoassinado para se autenticar para sistemas de site. Esta opção será selecionada automaticamente se você selecionar **Somente HTTPS**.  

    Quando os clientes são detectados na Internet ou estão configurados para gerenciamento de cliente apenas de Internet, eles sempre usam um certificado PKI de cliente.  

6.  Clique em **Modificar** para configurar o método de seleção de cliente escolhido para quando houver mais de um certificado de cliente PKI válido disponível em um cliente, e clique em **OK**.  

    Para obter mais informações sobre o método de seleção de certificado do cliente, consulte [Planejando a seleção de certificado de cliente PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Marque ou desmarque a caixa de seleção para os clientes verificarem a CRL (lista de certificados revogados).  

    Para obter mais informações sobre a verificação de CRL por parte dos clientes, consulte [Planejando a revogação de certificado PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Se for necessário especificar certificados de autoridade de certificação (AC) raiz confiáveis para clientes, clique em **Definir**, importe os arquivos de certificado AC raiz e clique em **OK**.  

    Para obter mais informações sobre essas configurações, consulte [Planejando certificados PKI de raiz confiável e a lista de emissores de certificados](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  

Repita esse procedimento para todos os sites primários da hierarquia.  

##  <a name="a-namebkmkconfiguresigningencryptiona-configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Configurar assinatura e criptografia  
Defina as configurações de assinatura e criptografia mais seguras para sistemas de site, às quais todos os clientes do site deem suporte. Essas configurações são especialmente importantes quando você permite que os clientes se comuniquem com sistemas de site usando certificados autoassinados por meio de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar assinatura e criptografia para um site  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**, clique em **Sites**e depois no site primário a ser configurado.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**e clique na guia **Assinatura e Criptografia** .  

    Essa guia está disponível somente em site primário. Se você não vir a guia **Assinatura e Criptografia** , verifique se você não está conectado a um site de administração central ou um site secundário.  

4.  Configure as opções de assinatura e criptografia desejadas e clique em **OK**.  

    > [!WARNING]  
    >  Não selecione **Exigir SHA-256** sem antes verificar se todos os clientes que podem ser atribuídos ao site oferecem suporte a esse algoritmo de hash ou se eles têm um certificado de autenticação de cliente PKI válido. Talvez você precise instalar atualizações ou hotfixes nos clientes para dar suporte ao SHA-256. Por exemplo, computadores que executam Windows Server 2003 SP2 devem instalar um hotfix que é referido no [KB artigo 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Se você selecionar essa opção e os clientes não derem suporte a SHA-256 e usarem certificados autoassinados, o Configuration Manager os rejeitará. Nesse cenário, o componente SMS_MP_CONTROL_MANAGER registra a identificação 5443 da mensagem.  

5.  Clique em **OK** para fechar a caixa de diálogo **Propriedades** do site.  

Repita esse procedimento para todos os sites primários da hierarquia.  

##  <a name="a-namebkmkconfigurerbaa-configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Configurar administração baseada em funções  
A administração baseada em funções combina funções de segurança, escopos de segurança e coleções atribuídas para definir o escopo administrativo para cada usuário administrativo. Um escopo administrativo inclui os objetos que um usuário administrativo pode exibir no console do Configuration Manager e as tarefas relacionadas a esses objetos que o usuário administrativo tem permissão para realizar. As configurações de administração baseada em funções são aplicadas em cada site de uma hierarquia.  

Os links a seguir destinam-se às seções relevantes do tópico [Configurar administração baseada em funções para o System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md):  

-   [Criar funções de segurança personalizadas](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurar escopos de segurança para um objeto](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerenciar a segurança](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Criar um novo usuário administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modificar o escopo administrativo de um usuário administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Seu próprio escopo administrativo define os objetos e as configurações que você pode atribuir ao configurar a administração baseada em funções para outro usuário administrativo. Para obter informações sobre como planejar a administração baseada em funções, consulte [Fundamentos de administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="a-namebkmkmanageaccountsa-manage-accounts-that-are-used-by-configuration-manager"></a><a name="BKMK_ManageAccounts"></a> Gerenciar contas usadas pelo Configuration Manager  
O Configuration Manager dá suporte a contas do Windows para várias tarefas e usos diferentes.  

Use o procedimento a seguir para exibir quais contas estão configuradas para tarefas diferentes e para gerenciar a senha que o Configuration Manager usa para cada conta.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Para gerenciar contas usadas pelo Gerenciador de Configurações  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Segurança**e clique em **Contas** para exibir as contas que estão configuradas para o Configuration Manager.  

3.  Para alterar a senha de uma conta que está configurada para o Configuration Manager, selecione a conta.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Clique em **Definir** para abrir a caixa de diálogo **Conta de Usuário do Windows** e especifique a nova senha para o Configuration Manager usar para a conta.  

    > [!NOTE]  
    >  A senha que você especificar deverá corresponder à senha especificada para a conta em Usuários e Computadores do Active Directory.  

6.  Clique em **OK** para concluir o procedimento.  



<!--HONumber=Dec16_HO3-->

