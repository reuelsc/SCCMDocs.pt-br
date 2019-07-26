---
title: Perguntas frequentes sobre produtos e licenciamento
titleSuffix: Configuration Manager
description: Encontre respostas para perguntas comuns sobre produtos e licenças do System Center Configuration Manager.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c0975c2b8dcf945464273930073ebf370bd4c32
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340165"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Perguntas frequentes sobre licenças e branches do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual), System Center Configuration Manager (Branch de Manutenção de Longo Prazo)*

Estas perguntas frequentes abordam o licenciamento de versões de branch atual e LTSB (branch de manutenção em longo prazo) do Configuration Manager, disponíveis por meio de programas de Licenciamento por volume da Microsoft. Este artigo é apenas informativo. Ele não substitui qualquer documentação sobre o licenciamento do System Center Configuration Manager. Para saber mais, veja o licenciamento de produto para o [System Center 2016](https://www.microsoft.com/en-us/licensing/product-licensing/system-center-2016.aspx)<!-- this link doesn't work without some language code --> e os [Termos do produto](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Os Termos do Produto descrevem os termos de uso para todos os produtos da Microsoft no licenciamento por volume.

Para saber mais sobre os recursos do System Center Configuration Manager, veja a [página do produto](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).



### <a name="bkmk_cb"></a> O que é o branch atual?  

Branch atual é o build pronto para produção do Configuration Manager que fornece um modelo de serviço ativo. Esse modelo de serviço é como a experiência com o Windows 10. Essa abordagem dá suporte aos clientes que estão se movendo em uma "cadência de nuvem" e desejam inovar de forma mais rápida. Com o modelo de serviço de branch atual, você continua a receber novos recursos e funcionalidades. Por esse motivo, apenas os clientes com Software Assurance ativo nas licenças do Configuration Manager ou com direitos de assinatura equivalente podem instalar e usar o branch atual do Configuration Manager.


### <a name="bkmk_ltsb"></a> O que é o LTSB (Branch de Manutenção em Longo Prazo)?  

O LTSB é uma compilação pronta para produção do Configuration Manager. Ele se destina a clientes que permitiram que seu Software Assurance ou seus direitos de assinatura equivalente prescrevessem. Em comparação com o branch atual, o LTSB tem [funcionalidade reduzida](/sccm/core/understand/introduction-to-the-ltsb#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Os clientes que permitem que o Software Assurance ou direitos de assinatura equivalente expirem devem desinstalar o branch atual do Configuration Manager. Clientes que têm direitos perpétuos do Configuration Manager podem instalar e utilizar o build LTSB da versão do Configuration Manager que for atual no momento em que a licença expirar.


### <a name="bkmk_licensing-acronyms"></a> Já vi os termos *SA* e *L&SA* sendo usados em conteúdos sobre licenciamento. O que significam esses acrônimos em relação ao Configuration Manager?    

Tanto SA **(Software Assurance)** quanto L&SA **(Licença e Software Assurance)** são opções de licença que concedem direitos de uso Configuration Manager. SA é uma opção para clientes que estão renovando a cobertura de SA de um contrato anterior. L&SA é uma opção para clientes que estão comprando uma nova licença e cobertura de SA.

- **SA (Software Assurance)** : os clientes devem ter o SA ativo para as licenças do Configuration Manager ou direitos de assinatura equivalentes para instalar e usar a opção de branch atual do Configuration Manager.    

  - Embora o SA seja opcional para alguns produtos da Microsoft, a única maneira de obter direitos de usar o branch atual do Configuration Manager é com o SA *ou direitos de assinatura equivalente*. Para saber mais, veja as [perguntas frequentes sobre o Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/FAQ-Software-Assurance.aspx).<!--this link doesn't work without some language code-->

- **L&SA (Licença e Software Assurance) da Microsoft**: clientes que estiverem comprando novas licenças do Configuration Manager devem adquirir a L&SA (a licença e a cobertura do SA).   

  - O SA concede direitos de uso do branch atual.

  - No entanto, se o seu SA expirar e você ainda tiver uma licença do Configuration Manager, não poderá mais usar o branch atual. Para mais informações, veja a pergunta frequente [O que acontece se meu SA expirar e eu tiver L&SA?](#bkmk_sa-expires)

Para saber mais sobre as ofertas de licença, veja [Maneiras de comprar](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs)<!--this link doesn't work without some language code--> e os [Termos de licenciamento de produtos](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  


### <a name="bkmk_equiv-sub"></a> Li o termo "assinatura equivalente", a quais programas ele se refere?   

Assinaturas equivalentes são referentes a programas como EMS [(Enterprise Mobility + Security)](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) ou [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Pode haver outros, mas esses programas são os mais comuns. Os Termos de Produto do Licenciamento por Volume da Microsoft se referem a esses programas como Licenças Equivalentes a Licença de Gerenciamento.


### <a name="bkmk_ems-expires"></a> Tenho o Enterprise Mobility + Security e ele expirou, o que devo fazer agora?  

O EMS concede direitos de uso do branch atual e do branch de manutenção em longo prazo do Configuration Manager. Quando esses direitos expirarem, você não tem mais direitos para usar qualquer Branch e deve desinstalá-los.  


### <a name="bkmk_sa-expires"></a> O que acontece se meu SA expirar e eu tiver L&SA?   

Se o seu SA expirou após 1º de outubro de 2016, dependendo sob qual programa você adquiriu L&SA, você pode manter uma licença perpétua para usar o LTSB. Se você utiliza o branch atual, desinstale-o e instale o LTSB. Não há suporte para migração ou conversão do branch atual para o LTSB.

Se o seu SA expirou antes de 1º de outubro de 2016 e você manteve uma licença perpétua para o Configuration Manager, sua única opção para uso contínuo é instalar e usar o System Center 2012 R2 Configuration Manager e seus pacotes de serviços disponíveis. Quando o seu SA expirou, você precisou desinstalar o branch atual e reinstalar a versão anterior do produto. Não há suporte para migrar ou fazer downgrade do branch atual do Configuration Manager para versões anteriores do Configuration Manager.   

Se você usar o System Center Endpoint Protection e seu SA expirar, será necessário reinstalá-lo. O System Center Endpoint Protection não oferece direitos *L (Licença)* e não há direitos perpétuos.<!--506238--> 


### <a name="bkmk_owncb"></a> Eu sou o "proprietário" do branch atual?   

Não. Você está licenciado para usar o branch atual enquanto seu SA estiver ativo. Por exemplo, via *L&SA*, quando o *SA* expira, você tem apenas direitos de *L (Licença)* , os quais não incluem direitos de uso do branch atual. Se o seu L fornece direitos perpétuos, você pode usar o LTSB do Configuration Manager no lugar do branch atual. Se o seu SA expirou antes de 1º de outubro de 2016, você também pode usar o System Center 2012 R2 Configuration Manager.


### <a name="bkmk_standalone"></a> Posso adquirir o Configuration Manager Standalone sem SA?      

Não. A única maneira de obter direitos de uso do Configuration Manager é adquirir uma licença com SA ou por meio de uma assinatura equivalente. Há programas do desenvolvedor, como o MSDN, no qual o Configuration Manager é oferecido para fins de desenvolvimento e teste, mas não paro uso em produção.


### <a name="bkmk_update-rights"></a> Vejo a oferta de atualizações para o Configuration Manager no meu console, como a versão 1810. Eu tenho direitos para instalá-las?   

Se o *SA* estiver ativo, você terá os direitos. Se o SA não estiver ativo, desinstale o branch atual e instale o LTSB do Configuration Manager. O LTSB não recebe atualizações para versões incrementais do Configuration Manager, mas recebe atualizações de segurança com base no ciclo de vida de suporte.


### <a name="bkmk_csp"></a> Eu comprei o EMS ou Microsoft 365 por meio de um CSP (Provedor de Solução de Nuvem), tenho direitos para usar o Configuration Manager? 

Sim, você tem direitos para usar o Configuration Manager para gerenciar clientes abordados pela licença do EMS. Primeiramente, baixe e instale o [software de avaliação](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Em seguida, entre em contato com o Suporte da Microsoft para obter a chave de licença.<!--issue472--> Ao conversar com o Suporte da Microsoft, peça que confira o artigo interno com ID 4033838.<!-- SCCMDocs issue 493 --> 


### <a name="bkmk_expiration-date"></a> A data de término da minha assinatura é a mesma que a data de validade do SA?    

Se o *SA* ou sua assinatura estiverem ativos, você terá direitos de uso do branch atual do Configuration Manager. Uma assinatura ativa é equivalente a ter um *SA* ativo, mas não é uma *"L" (licença)* perpétua. Quando sua assinatura terminar, desinstale o branch atual. Neste momento, você não tem direito de uso do LTSB.  


### <a name="bkmk_sql"></a> Quais são os direitos de uso associados à tecnologia SQL fornecida com o Configuration Manager?    

Todos os produtos do System Center incluem a tecnologia do SQL Server. Os termos de licenciamento da Microsoft para esses produtos permitem o uso da tecnologia SQL Server por parte do cliente apenas para dar suporte a componentes do System Center. As licenças de acesso de cliente do SQL Server não são necessárias para isso. 
 
Os direitos de uso aprovados para os recursos do SQL com o Configuration Manager incluem:
- Função de banco de dados do site
- O WSUS (Windows Server Update Services) para a função de ponto de atualização de software
- O SQL Server Reporting Services (SSRS) para a função de ponto de relatório
- Função do ponto de serviço do Data Warehouse
- Réplicas de banco de dados para funções de ponto de gerenciamento
- AlwaysOn do SQL Server 

A licença do SQL Server incluída no Configuration Manager oferece suporte a cada instância do SQL Server que você instala para hospedar um banco de dados do Configuration Manager. No entanto, apenas os bancos de dados para o Configuration Manager da lista anterior poderão executar nesse SQL Server quando você usar essa licença. Se um banco de dados de qualquer produto de terceiros ou adicional da Microsoft compartilhar o SQL Server, você deverá ter uma licença separada para essa instância do SQL Server. 
 <!-- sms500967 -->


### <a name="bkmk_opmdm"></a> O MDM (gerenciamento de dispositivo móvel) local exige uma assinatura do Intune?

Na versão 1806 e anteriores, para começar a usar o MDM local, você precisa de uma assinatura do Microsoft Intune. A assinatura apenas é necessária para acompanhar o licenciamento dos dispositivos e não é usada para gerenciar ou armazenar informações de gerenciamento dos dispositivos. Todos os dados de gerenciamento são armazenados em sua organização usando a infraestrutura do Configuration Manager local.  

A partir da versão 1810, não é mais necessário ter uma conexão do Intune para novas implantações locais do MDM.<!--3607730, fka 1359124--> Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, não é possível remover a conexão do Intune das implantações de MDM locais existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

