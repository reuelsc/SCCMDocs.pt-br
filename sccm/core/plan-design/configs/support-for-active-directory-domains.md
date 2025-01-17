---
title: Domínios do Active Directory com suporte
titleSuffix: Configuration Manager
description: Obtenha os requisitos para a associação de um sistema de sites do System Center Configuration Manager em um domínio do Active Directory.
ms.date: 9/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02353e516e7af45afe273bc0deff5b227a7c7f2c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499435"
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>Domínios do Active Directory com suporte no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Todos os sistemas de sites do System Center Configuration Manager devem ser membros de um domínio do Active Directory do Windows Server com suporte. Os computadores cliente do Configuration Manager podem ser membros do domínio ou membros do grupo de trabalho.  

 **Requisitos e limitações:**  

-   A associação ao domínio se aplica a sistemas de sites que dão suporte ao gerenciamento de clientes baseado na Internet em uma rede de perímetro (também conhecida como um DMZ, zona desmilitarizada e sub-rede filtrada).  

-   Não há suporte para alterar o seguinte em um computador que hospeda uma função do sistema de sites:  

    -   Associação de domínio *(Isso inclui remover um sistema de site do domínio e, em seguida, reassociar o mesmo domínio).*

    -   Nome de domínio  

    -   Nome do computador  

É necessário desinstalar a função do sistema de sites (incluindo o site, caso seja um servidor do site) antes de fazer essas alterações.  

**Há suporte para domínios com os seguintes níveis funcionais de domínio:**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Namespace não contíguo  
O Configuration Manager dá suporte à instalação de sistemas de sites e clientes em um domínio com namespace não contíguo.  

Um cenário de namespace não contíguo é aquele em que o sufixo DNS (Sistema de Nomes de Domínio) primário de um computador não corresponde ao nome de domínio DNS do Active Directory em que o computador reside. O computador que usa o sufixo DNS primário sem correspondência é chamado não contíguo. Outro cenário de namespace não contíguo ocorrerá se o nome de domínio NetBIOS de um controlador de domínio não corresponder ao nome de domínio DNS do Active Directory.  

A tabela a seguir identifica os cenários com suporte para um namespace não contíguo.  

|Cenário|Mais informações|  
|--------------|----------------------|  
|**Cenário 1:**<br /><br /> O sufixo DNS primário do controlador de domínio é diferente do nome de domínio DNS do Active Directory. Os computadores que são membros do domínio podem ser contíguos ou não contíguos.|Neste cenário, o sufixo DNS primário do controlador de domínio é diferente do nome de domínio DNS do Active Directory. O controlador de domínio é não contíguo neste cenário. Os computadores que são membros do domínio, como servidores do site e computadores, podem ter um sufixo DNS primário que corresponde ao sufixo DNS primário do controlador de domínio ou que corresponde ao nome de domínio DNS do Active Directory.|  
|**Cenário 2:**<br /><br /> Um computador membro em um domínio do Active Directory é não contíguo, embora o controlador de domínio não seja contíguo.|Neste cenário, o sufixo DNS primário de um computador membro no qual um sistema de sites está instalado é diferente do nome de domínio DNS do Active Directory, mesmo que o sufixo DNS primário do controlador de domínio seja o mesmo que o nome de domínio DNS do Active Directory. Neste cenário, você tem um controlador de domínio contíguo e um computador membro não contíguo. Os computadores membros que executam o cliente do Configuration Manager podem ter um sufixo DNS primário que corresponde àquele do servidor do sistema de sites não contíguo ou que corresponde ao nome de domínio DNS do Active Directory.|  

 Para permitir que um computador acesse os controladores de domínio não contíguos, você deve alterar o atributo **msDS-AllowedDNSSuffixes** do Active Directory no contêiner do objeto de domínio. É necessário adicionar os dois sufixos DNS ao atributo.  

 Além disso, para garantir que a lista de pesquisa de sufixos DNS contém todos os namespaces DNS implantados na organização, é necessário configurar a lista de pesquisa para cada computador no domínio não contíguo. Lembre-se de incluir o seguinte na lista de namespaces: o sufixo DNS primário do controlador de domínio, o nome de domínio DNS e todos os namespaces adicionais para outros servidores com os quais o Configuration Manager poderá interoperar. É possível usar o Console de Gerenciamento de Política de Grupo para configurar a lista **pesquisa de sufixos do DNS (Sistema de Nomes de Domínio)** .  

> [!IMPORTANT]  
>  Ao fazer referência a um computador no Configuration Manager, insira o computador usando seu sufixo DNS Primário. Esse sufixo deve corresponder ao Nome de Domínio Totalmente Qualificado registrado como o atributo **dnsHostName** no domínio do Active Directory e ao Nome da Entidade de Serviço associado ao sistema.  

##  <a name="bkmk_SLD"></a> Domínios de rótulo único  
 O Configuration Manager dá suporte a sistemas de sites e clientes em um domínio de rótulo único quando os critérios a seguir são atendidos:  

-   O domínio de rótulo único no Active Directory Domain Services deve ser configurado com um namespace DNS não contíguo que tem um domínio primário válido.  

     **Por exemplo:** o domínio de rótulo único da Contoso é configurado para ter um namespace não contíguo no DNS de contoso.com. Portanto, ao especificar o sufixo DNS no Configuration Manager para um computador no domínio Contoso, especifique “Contoso.com” e não “Contoso”.  

-   As conexões do DCOM (Distributed Component Object Model) entre os servidores do site no contexto do sistema devem ser bem-sucedidas com o uso da autenticação Kerberos.  
