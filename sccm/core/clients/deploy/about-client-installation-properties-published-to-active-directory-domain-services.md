---
title: "Propriedades de instalação de cliente no Active Directory Domain Services | Microsoft Docs"
description: "Use as propriedades de instalação de cliente publicadas no Active Directory Domain Services no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bc610b495047c49853c0a8f478cbf2773c0d3603
ms.openlocfilehash: e50095ef618ec40a51c29ef2c8116f8e07401bd1

---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando você estende o esquema do Active Directory para o System Center Configuration Manager e o site é publicado no Active Directory Domain Services, muitas propriedades de instalação do cliente são publicadas neles. Se um computador puder localizar essas propriedades de instalação do cliente, ele poderá usá-las durante a implantação do cliente do Configuration Manager.  

 As vantagens de usar os Serviços de Domínio Active Directory para publicar propriedades de instalação de cliente são as seguintes:  

-   A instalação do cliente baseada em ponto de atualização do software e as instalações de cliente da Política de Grupo não exigem que os parâmetros de configuração sejam configurados em cada computador.  

-   Como essa informação é gerada automaticamente, o risco de erro humano associado à inserção manual de propriedades de instalação é eliminado.  

> [!NOTE]  
>  Para saber mais sobre como estender o esquema do Active Directory para o Configuration Manager e como publicar um site, consulte [Extensões de esquema para o System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propriedades de instalação de cliente publicadas no Active Directory Domain Services  
Veja a seguir uma lista de propriedades de instalação do cliente. Para saber mais sobre cada item listado abaixo, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   O código do site do Configuration Manager.  

-   O certificado de autenticação do servidor de site.  

-   A chave de raiz confiável.  

-   As portas de comunicação do cliente para HTTP e HTTPS.  

-   O ponto de status de fallback. Se o site tiver diversos pontos de status de fallback, somente o primeiro instalado será publicado nos Active Directory Domain Services.  

-   Uma configuração para indicar que o cliente deve se comunicar somente por meio de HTTPS.  

-   Configurações relacionadas a certificados PKI:  

   -   Se é necessário usar um certificado PKI do cliente.  

   -   Os critérios de seleção para seleção do certificado. Isso pode ser exigido, pois o cliente tem mais de um certificado PKI válido que pode ser usado para o Configuration Manager.  

   -   Uma configuração para determinar qual certificado usar se o cliente tiver vários certificados válidos após o processo de seleção de certificados.  

   -   A lista de emissores do certificado que contém uma lista de certificados de autoridade de certificação raiz confiável.  

-   Propriedades da instalação client.msi especificadas na guia **Cliente** da caixa de diálogo **Propriedades da Instalação do Cliente por Push** .

A instalação de cliente (CCMSetup) utilizará as propriedades publicadas no Active Directory Domain Services somente se nenhuma outra propriedade for especificada usando um dos métodos a seguir:  

-   O método de instalação manual (descrito posteriormente neste artigo)

-   O método de instalação manual de Política de Grupo (descrito posteriormente neste artigo)

> [!NOTE]  
>  As propriedades de instalação de cliente são usadas para instalar o cliente. Essas propriedades poderão ser substituídas por novas configurações de seu site atribuído após o cliente ser instalado e atribuído com êxito a um site do Configuration Manager.  

 Use a tabela a seguir para determinar quais métodos de instalação do cliente do Configuration Manager usam o Active Directory Domain Services para obter as propriedades de instalação do cliente.  

## <a name="client-push-installation"></a>Instalação do cliente por push  
 A instalação do cliente por push não usa os Serviços de Domínio Active Directory para obter as propriedades de instalação.  

 Em vez disso, é possível especificar propriedades de instalação cliente na guia **Cliente** da caixa de diálogo **Propriedades da Instalação do Cliente por Push** . Essas opções e configurações relacionadas ao cliente estão armazenadas em um arquivo que o cliente lê durante a instalação de cliente.  

> [!NOTE]  
>  Não é necessário especificar nenhuma propriedade do CCMSetup para a instalação do cliente por push, ou o ponto de status de fallback, ou a chave de raiz confiável na guia **Cliente** . Essas configurações são fornecidas automaticamente para os clientes quando eles são instalados pela instalação de cliente por push.  

 Qualquer propriedade especificada na guia **Cliente** será publicada nos Active Directory Domain Services se o site for publicado nos Active Directory Domain Services. Essas configurações são lidas por instalações de cliente nas quais o CCMSetup é executado sem propriedades de instalação.  

## <a name="software-update-point-based-installation"></a>Instalação baseada em ponto de atualização de software  
 O método de instalação baseado em ponto de atualização de software não oferece suporte à adição de propriedades de instalação à linha de comando CCMSetup.  

 Se nenhuma propriedade de linha de comando for fornecida no computador cliente usando a Política de Grupo, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio Active Directory.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 O método de instalação de Política de Grupo não dá suporte para a adição de propriedades de instalação à linha de comando CCMSetup.  

 Se nenhuma propriedade de linha de comando for fornecida no computador cliente, o CCMSetup procurará as propriedades de instalação nos Serviços de Domínio Active Directory.  

## <a name="manual-installation"></a>Instalação manual  
 O CCMSetup procura as propriedades de instalação nos Serviços de Domínio Active Directory nas seguintes circunstâncias:  

-   Nenhuma propriedade de linha de comando é especificada após o comando CCMSetup.exe.  

-   O computador não foi provisionado com as propriedades de instalação usando a Política de Grupo.  

## <a name="logon-script-installation"></a>Instalação de script de logon  
 O CCMSetup procura as propriedades de instalação nos Serviços de Domínio Active Directory nas seguintes circunstâncias:  

-   Nenhuma propriedade de linha de comando é especificada após o comando CCMSetup.exe.  

-   O computador não foi provisionado com as propriedades de instalação usando a Política de Grupo.  

## <a name="software-distribution-installation"></a>Instalação de distribuição do software  
 O CCMSetup procura as propriedades de instalação nos Serviços de Domínio Active Directory nas seguintes circunstâncias:  

-   Nenhuma propriedade de linha de comando é especificada após o comando CCMSetup.exe.  

-   O computador não foi provisionado com as propriedades de instalação usando a Política de Grupo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Instalações para clientes que não podem acessar o Active Directory Domain Services  
Esses computadores cliente não podem ler ou acessar as propriedades de instalação publicadas a partir dos Active Directory Domain Services.

 Esses clientes incluem:  

-   Computadores do grupo de trabalho.  

-   Clientes que são atribuídos a um site do Configuration Manager que não está publicado no Active Directory Domain Services.  

-   Clientes que são instalados quando estão na Internet.  



<!--HONumber=Dec16_HO3-->


