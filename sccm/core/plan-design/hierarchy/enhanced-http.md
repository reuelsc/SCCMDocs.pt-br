---
title: HTTP aprimorado
titleSuffix: Configuration Manager
description: Use autenticação moderna para proteger a comunicação do cliente sem a necessidade de certificados PKI.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f2fab639082e6871e5df8dcebe0d1b3a440624c
ms.sourcegitcommit: 1bf26b83fa7da637d299a21e1d3bc61f2d7d8c10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2019
ms.locfileid: "54060358"
---
# <a name="enhanced-http"></a>HTTP aprimorado

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1356889,1358460-->

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão 1806 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Na versão 1810, esse recurso deixou de ser um recurso de pré-lançamento.  


A Microsoft recomenda usar comunicação HTTPS para todos os caminhos de comunicação do Configuration Manager, mas pode ser um desafio para alguns clientes devido à sobrecarga de gerenciamento de certificados PKI. A introdução da integração do Azure AD (Azure Active Directory) reduz alguns, mas não todos os requisitos de certificado. 

O Configuration Manager versão 1806 inclui melhorias em como os clientes se comunicam com sistemas de site. Há dois objetivos principais para essas melhorias:  

- Você pode proteger comunicação confidencial do cliente sem necessidade de certificados de autenticação do servidor PKI.  

- Os clientes podem acessar com segurança o conteúdo dos pontos de distribuição sem necessidade de uma conta de acesso à rede, certificado PKI de cliente nem autenticação do Windows.  

> [!Note]  
> Certificados PKI ainda são uma opção válida para clientes com os seguintes requisitos:   
> - Toda a comunicação de cliente é por HTTPS  
> - Controle avançado da infraestrutura de assinatura  


## <a name="bkmk_scenario"></a> Cenários

Os cenários a seguir se beneficiam dessas melhorias:  


### <a name="bkmk_scenario1"></a> Cenário 1: cliente para o ponto de gerenciamento
<!--1356889-->

[Dispositivos que ingressaram no Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) podem se comunicar com um ponto de gerenciamento configurado para HTTP. O servidor do site gera um certificado para o ponto de gerenciamento, permitindo que ele se comunique por meio de um canal seguro.   

> [!Note]  
> Esse comportamento mudou com relação à atual branch do Configuration Manager versão 1802, que exige um ponto de gerenciamento habilitado para HTTPS para clientes que ingressaram no Azure AD se comunicarem por meio de um gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Habilitar ponto de gerenciamento para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_scenario2"></a> Cenário 2: cliente para o ponto de distribuição
<!--1358228-->

Um cliente que ingressou no Azure AD ou no grupo de trabalho pode autenticar-se e baixar o conteúdo por meio de um canal seguro de um ponto de distribuição configurado para HTTP. Esses tipos de dispositivos também podem autenticar e baixar conteúdo de um ponto de distribuição configurado para HTTPS sem necessidade de um certificado PKI no cliente. É um desafio adicionar um certificado de autenticação de cliente a um grupo de trabalho ou um cliente que ingressou no Azure AD.

Esse comportamento inclui cenários de implantação de sistema operacional com uma sequência de tarefas em execução no Centro de Software, PXE ou mídia de inicialização. Para obter mais informações, confira [Conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).<!--1358278-->


### <a name="bkmk_scenario3"></a> Cenário 3: Identidade do dispositivo do Azure AD 
<!--1358460-->

Um [dispositivo do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) ou que ingressou no Azure AD sem um usuário do Azure AD conectado pode se comunicar com segurança com o site atribuído. A identidade do dispositivo baseado em nuvem agora é suficiente para autenticar com o CMG e o ponto de gerenciamento para cenários centrados em dispositivo. (Um token de usuário ainda é necessário para cenários centrados no usuário.)  


## <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gerenciamento configurado para conexões de cliente HTTP. Defina essa opção na guia **Geral** das propriedades da função do sistema de sites.  

- Um ponto de distribuição configurado para conexões de cliente HTTP. Defina essa opção na guia **Geral** das propriedades da função do sistema de sites. Não habilite a opção para **Permitir que os clientes se conectem anonimamente**.  

- Integrar o site ao Azure AD para gerenciamento de nuvem.  

    - Se você já tiver cumprido esse pré-requisito para o seu site, precisará atualizar o aplicativo do Azure AD. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione **Locatários do Azure Active Directory**. Selecione o locatário do Azure AD, selecione o aplicativo Web no painel **​​Aplicativos** e selecione em **Atualizar configuração de aplicativo** na faixa de opções.  

- *Somente para o [Cenário 3](#bkmk_scenario3)*: Um cliente que executa o Windows 10 versão 1803 ou posterior e ingressou no Azure AD. 



## <a name="configure-the-site"></a>Configurar o site

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site e escolha em **Propriedades** na faixa de opções.  

2. Alterne para a guia **Comunicação do Computador Cliente**. Selecione a opção para **HTTPS ou HTTP** e, em seguida, habilite a opção para **Usar certificados gerados pelo Configuration Manager para sistemas de site HTTP**.  

> [!Tip]
> Aguarde até 30 minutos para o ponto de gerenciamento receber e configurar o novo certificado do site.

Você pode ver esses certificados no console do Configuration Manager. Acesse o workspace **Administração**, expanda **Segurança** e selecione o nó **Certificados**. Procure o certificado raiz **Emissão de SMS**, bem como os certificados de função de servidor do site emitidos pela raiz de emissão do SMS.

Para obter mais informações sobre como o cliente se comunica com o ponto de gerenciamento e o ponto de distribuição com essa configuração, confira [Comunicações de clientes para sistemas de sites e serviços](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System).



## <a name="see-also"></a>Consulte também
- [Planejar a segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Segurança e privacidade para clientes do Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurar a segurança](/sccm/core/plan-design/security/configure-security)  

- [Comunicação entre pontos de extremidade](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

