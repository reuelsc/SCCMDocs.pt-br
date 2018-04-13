---
title: Visão geral dos certificados CNG
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte para certificados CNG (Cryptography Next Generation) em clientes e servidores do Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 271cc0e2753f1a65740187a4faf6875c1a018014
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="cng-certificates-overview"></a>Visão geral dos certificados CNG
<!-- 1356191 --> 

O Configuration Manager tem um suporte limitado para certificados CNG (Cryptography Next Generation). Os clientes do Configuration Manager podem usar o certificado de autenticação de cliente de PKI com chave privada no KSP (provedor de armazenamento de chaves) da CNG. Com o suporte do KSP, os clientes do Configuration Manager dão suporte para chave de privada baseada em hardware, como TPM KSP para certificados de autenticação de cliente de PKI.

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode usar modelos de certificado [CNG (Cryptography API: Next Generation)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) para os seguintes cenários:

- Registro de cliente e comunicação com um ponto de gerenciamento HTTPS   
- Distribuição de software e implantação de aplicativos com um ponto de distribuição HTTPS   
- Implantação de sistema operacional  
- SDK de mensagens do cliente (com a última atualização) e Proxy de ISV   
- Configuração do Gateway de Gerenciamento de Nuvem  

A partir da versão 1802, use certificados CNG para as seguintes funções de servidor habilitadas para HTTPS: <!-- 1357314 -->   
- Ponto de gerenciamento
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de migração de estado     

> [!NOTE]
> A CNG é compatível com versões anteriores com CAPI (Crypto API). Os certificados CAPI continuam com suporte mesmo quando o suporte para CNG está habilitado no cliente.

## <a name="unsupported-scenarios"></a>Cenários sem suporte

No momento, não há suporte para os seguintes cenários:

- As seguintes funções de servidor não são operacionais quando instaladas no modo HTTPS com um certificado CNG associado ao site no IIS (Serviços de Informações da Internet): 
    - Serviço Web do catálogo de aplicativos
    - Site da Web do catálogo de aplicativos
    - Ponto de registro  
    - Ponto proxy do registro  

- O Centro de Software não exibe como disponíveis os aplicativos e os pacotes que são implantados em coleções de usuário ou de grupo de usuários.

- Usando certificados CNG para criar um ponto de distribuição de nuvem.

- Se o módulo de política do NDES estiver usando um certificado CNG para a autenticação de cliente, a comunicação com o ponto de registro de certificado falhará.

- Se você especificar um certificado CNG ao criar a mídia de sequência de tarefas, o assistente não criará uma mídia inicializável.

## <a name="to-use-cng-certificates"></a>Para usar certificados CNG

Para usar os certificados CNG, sua CA (autoridade de certificação) precisa fornecer modelos de certificado de CNG para computadores de destino. Os detalhes do modelo variam de acordo com o cenário. No entanto, as propriedades a seguir são obrigatórias:

- Guia **Compatibilidade**

    - **Autoridade de Certificação** deve ser Windows Server 2008 ou posterior. (Recomendamos o Windows Server 2012.)

    - **Destinatário de certificação** deve ser Windows Vista/Server 2008 ou posterior. (Recomendamos o Windows 8/Windows Server 2012.)

- Guia **Criptografia**

    - **Categoria de Provedor** devem ser **Provedor de armazenamento de chaves**. (obrigatório)

> [!NOTE]
> Os requisitos de seu ambiente ou da sua organização podem ser diferentes. Contate seu especialista em PKI. O ponto importante a ser considerado é que um modelo de certificado deve usar um provedor de armazenamento de chaves para usufruir da CNG.

Para obter os melhores resultados, recomendamos a criação do Nome da Entidade a partir de informações do Active Directory. Use o Nome DNS para o **Formato de nome de entidade** e inclua o nome DNS no nome alternativo da entidade. Caso contrário, você deverá fornecer essas informações quando o dispositivo for registrado no perfil de certificado.