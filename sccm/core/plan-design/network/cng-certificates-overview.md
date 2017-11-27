---
title: "Visão geral dos certificados CNG"
titleSuffix: Configuration Manager
description: "Uma visão geral dos certificados CNG no Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>Visão geral dos certificados CNG
<!-- 1356191 --> 

O Configuration Manager tem um suporte limitado para certificados CNG (Cryptography Next Generation). Os clientes do Configuration Manager podem usar o certificado de autenticação de cliente de PKI com chave privada no KSP (provedor de armazenamento de chaves) da CNG. Com o suporte do KSP, os clientes do Configuration Manager dão suporte para chave de privada baseada em hardware, como TPM KSP para certificados de autenticação de cliente de PKI.

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode usar modelos de certificado [CNG (Cryptography API: Next Generation)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) para os seguintes cenários:

- O registro de cliente e a comunicação com um ponto de gerenciamento HTTPS.   
- Distribuição e o aplicativo de implantação de software com um ponto de distribuição HTTPS.   
- Implantação de sistema operacional.  
- SDK de mensagens do cliente (com a atualização mais recente) e Proxy ISV.   
- Configuração do Gateway de Gerenciamento de Nuvem.  

> [!NOTE]
> A CNG é compatível com versões anteriores com CAPI (Crypto API). Os certificados CAPI continuam com suporte mesmo quando o suporte para CNG está habilitado no cliente.

## <a name="unsupported-scenarios"></a>Cenários sem suporte

No momento, não há suporte para os seguintes cenários:

- O serviço Web do Catálogo de Aplicativos, o site do Catálogo de Aplicativos, o ponto do registro e as funções de ponto proxy do registro não funcionam quando a instalação ocorre no modo HTTPS com um certificado CNG associado ao site no IIS (Serviços de Informações da Internet). O Centro de Software não exibe como disponíveis os aplicativos e os pacotes que são implantados em coleções de usuário ou de grupo de usuários.

- O ponto de migração de estado não funciona quando a instalação ocorre no modo HTTPS com um certificado CNG associado ao site no IIS.

- Usando certificados CNG para criar um ponto de distribuição de nuvem.

- A comunicação do Módulo de Política do NDES com o CRP (Ponto de Registro do Certificado) falhará se o Módulo de Política do NDES estiver usando um certificado CNG para a certificado de autenticação de cliente.

- A criação da mídia de sequência de tarefas não conseguirá criar uma mídia inicializável se houver um certificado CNG especificado.

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