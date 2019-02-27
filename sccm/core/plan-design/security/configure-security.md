---
title: Configurar a segurança
titleSuffix: Configuration Manager
description: Configure as opções de segurança no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d58f8566f80efa2700f5947f4144623b10eb6ad
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140585"
---
# <a name="configure-security-in-configuration-manager"></a>Configurar a segurança no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste artigo para ajudá-lo a configurar as opções relacionadas à segurança para o Configuration Manager. Ele aborda as seguintes opções de segurança:
- [Comunicação do computador cliente](#BKMK_ConfigureClientPKI) para certificados PKI do cliente  
- [Assinatura e criptografia](#BKMK_ConfigureSigningEncryption)  
- [Administração baseada em funções](#BKMK_ConfigureRBA)  
- [Gerenciar contas](#BKMK_ManageAccounts)  
- [Configurar o Azure Active Directory](#bkmk_azuread)  
- [Configurar a autenticação do provedor de SMS](#bkmk_auth)  



##  <a name="BKMK_ConfigureClientPKI"></a> Definir configurações para certificados PKI de clientes  

Se você quiser usar certificados PKI (infraestrutura de chave pública) para conexões de clientes a sistemas de site que usam IIS (Serviços de Informações da Internet), use o procedimento a seguir para definir as configurações para esses certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para definir configurações de certificados PKI de clientes  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site primário a configurar.  

2.  Na faixa de opções, escolha **Propriedades**. Alterne então para a guia **Comunicação do Computador Cliente**.  

    Essa guia está disponível somente em site primário. Se não vir a guia **Comunicação de Computador Cliente**, assegure que você não está conectado a um site de administração central ou um site secundário.  

3.  Selecione as configurações de sistemas de sites que usam o IIS.  

    - **Somente HTTPS**: clientes atribuídos ao site sempre usam um certificado PKI de cliente ao se conectarem a sistemas de site que usam o IIS.  

    - **HTTPS ou HTTP**: você não exige que os clientes usem certificados PKI.  

    - **Use os certificados gerados pelo Configuration Manager para sistemas de sites HTTP**: Para saber mais sobre essa configuração, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).  

4.  Selecione as configurações para computadores cliente.  

    - **Usar o certificado PKI de cliente (funcionalidade de autenticação de cliente) quando disponível**: se você escolher a configuração de servidor do site **HTTP ou HTTPS**, escolha esta opção para usar um certificado PKI de cliente para conexões HTTP. O cliente usa esse certificado em vez de um certificado autoassinado para se autenticar para sistemas de site. Esta opção será escolhida automaticamente se você escolher **Somente HTTPS**.  

    Quando houver mais de um certificado de cliente PKI válido disponível em um cliente, escolha **Modificar** para configurar os métodos de seleção de certificado do cliente.  

    Para obter mais informações sobre o método de seleção de certificado do cliente, consulte [Planejando a seleção de certificado de cliente PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection).  

    - **Os clientes verificam a CRL (lista de certificados revogados) para sistemas de sites**: habilite essa configuração para que os clientes verifiquem a CRL da sua organização para certificados revogados.  

    Para obter mais informações sobre a verificação de CRL por parte dos clientes, consulte [Planejando a revogação de certificado PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).  

5.  Para importar, exibir e excluir os certificados de autoridades de certificação confiáveis, escolha **Definir**.  

    Para obter mais informações, confira [Planejando certificados PKI de raiz confiável e a lista de emissores de certificados](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs).  


Repita esse procedimento para todos os sites primários da hierarquia.  



##  <a name="BKMK_ConfigureSigningEncryption"></a> Configurar assinatura e criptografia  

Defina as configurações de assinatura e criptografia mais seguras para sistemas de site, às quais todos os clientes do site deem suporte. Essas configurações são especialmente importantes quando você permite que os clientes se comuniquem com sistemas de site usando certificados autoassinados por meio de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar assinatura e criptografia para um site  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site primário a configurar.  

2.  Na faixa de opções, selecione **Propriedades** e, em seguida, alterne para a guia **Assinatura e criptografia**.  

    Essa guia está disponível somente em site primário. Se você não vir a guia **Assinatura e Criptografia**, assegure que você não está conectado a um site de administração central ou um site secundário.  

3.  Configure as opções de assinatura e criptografia para que os clientes se comuniquem com o site.  

    - **Exigir assinatura**: os clientes assinem dados antes de enviá-los para o ponto de gerenciamento.  

    - **Exigir SHA-256**: os clientes usam o algoritmo SHA-256 durante a assinatura de dados.  

    > [!WARNING]  
    >  Não escolha **Exigir SHA-256** sem primeiro confirmar que todos os clientes dão suporte a esse algoritmo de hash. Esses clientes incluem aqueles que podem ser atribuídos ao site no futuro.  
    >   
    >  Se você escolher essa opção e os clientes com certificados autoassinados não derem suporte a SHA-256, o Configuration Manager os rejeitará. O componente SMS_MP_CONTROL_MANAGER registra a identificação 5443 da mensagem.  

    - **Usar criptografia**: os clientes criptografam mensagens de status e dados de inventário de cliente antes de enviar para o ponto de gerenciamento. Eles usam o algoritmo 3DES.  

Repita esse procedimento para todos os sites primários da hierarquia.  



##  <a name="BKMK_ConfigureRBA"></a> Configurar administração baseada em funções  

A administração baseada em funções combina funções de segurança, escopos de segurança e coleções atribuídas para definir o escopo administrativo para cada usuário administrativo. Um escopo inclui os objetos que um usuário pode exibir no console e as tarefas relacionadas a esses objetos que ele tem permissão para realizar. As configurações de administração baseada em funções são aplicadas em cada site de uma hierarquia.  

Para obter mais informações, confira [Configurar a administração baseada em função](/sccm/core/servers/deploy/configure/configure-role-based-administration). Este artigo fornece detalhes sobre as seguintes ações:  

- Criar funções de segurança personalizadas  

- Configurar funções de segurança  

- Configurar escopos de segurança para um objeto  

- Configurar coleções para gerenciar a segurança  

- Criar um novo usuário administrativo  

- Modificar o escopo administrativo de um usuário administrativo  

> [!IMPORTANT]  
>  Seu próprio escopo administrativo define os objetos e as configurações que você pode atribuir ao configurar a administração baseada em funções para outro usuário administrativo. Para obter informações sobre o planejamento para administração baseada em funções, confira [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  



##  <a name="BKMK_ManageAccounts"></a> Gerenciar contas usadas pelo Configuration Manager  

O Configuration Manager dá suporte a contas do Windows para várias tarefas e usos diferentes. Use o procedimento a seguir para exibir as contas que estão configuradas para tarefas diferentes e para gerenciar a senha que o Configuration Manager usa para cada conta:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Para gerenciar contas usadas pelo Configuration Manager  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Segurança** e escolha o nó **Contas**.  

2.  Para alterar a senha de uma conta, selecione a conta na lista. Depois, na faixa de opções, escolha **Propriedades**.  

3.  Escolha **Definir** para abrir a caixa de diálogo **Conta de Usuário do Windows**. Especifique a nova senha para o Configuration Manager usar para essa conta.  

    > [!NOTE]  
    >  A senha que você especificar deverá corresponder à senha dessa conta no Active Directory.  

Para obter mais informações, confira [Contas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).



##  <a name="bkmk_azuread"></a> Configurar o Azure Active Directory

Integre o Configuration Manager com o Azure AD (Azure Active Directory) para simplificar seu ambiente e habilitá-lo para a nuvem. Permita que os clientes autentiquem usando o Azure AD. Para obter mais informações, confira o serviço **Gerenciamento de Nuvem** em [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).



## <a name="bkmk_auth"></a> Configurar a autenticação do provedor de SMS

Da versão 1810 em diante, você pode especificar o nível mínimo de autenticação para os administradores acessarem sites do Configuration Manager. Esse recurso faz com que os administradores entrem no Windows com o nível necessário. Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Consulte também

- [Planejar a segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Referência técnica de controles de criptografia](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  
