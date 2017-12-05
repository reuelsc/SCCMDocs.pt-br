---
title: "Extensões de esquema"
titleSuffix: Configuration Manager
description: Estender o esquema do Active Directory para o System Center Configuration Manager.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: "8"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
robots: noindex
ms.openlocfilehash: 1fa1e3be3d08c9aa1f9271868f6b01e20b63e444
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensões de esquema para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode estender o esquema do Active Directory para dar suporte ao Configuration Manager. Isso edita o esquema do Active Directory de uma floresta para adicionar um novo contêiner e vários atributos que são usados por sites do Configuration Manager para publicar informações essenciais no Active Directory, onde os clientes podem acessá-las com segurança. Essas informações podem simplificar a implantação e a configuração de clientes e ajudam os clientes a localizarem recursos do site, como servidores com conteúdo implantado ou que fornecem vários serviços aos clientes.  

-   Recomenda-se estender o esquema do Active Directory, mas não é obrigatório.  

Antes de [estender o esquema do Active Directory](https://docs.microsoft.com/en-us/sccm/core/plan-design/network/extend-the-active-directory-schema), você deve estar familiarizado com os Serviços de Domínio do Active Directory e com [realizar alterações no esquema do Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considerações sobre estender o esquema do Active Directory para o Configuration Manager  

-   As extensões de esquema do Active Directory para o System Center Configuration Manager são as mesmas usadas pelo Configuration Manager 2007 e Configuration Manager 2012. Se tiver estendido o esquema anteriormente para alguma das versões, você não precisará estendê-lo novamente.  

-   A extensão do esquema é uma ação única e irreversível que afeta toda a floresta.  

-   A extensão do esquema deve ser feita apenas por um usuário que seja membro do Grupo de administradores de esquemas ou para o qual tenham sido delegadas permissões suficientes para modificar o esquema.  

-   Embora seja possível estender o esquema antes ou depois de executar a Instalação do Configuration Manager, é recomendável fazer isso antes de começar a configurar seus sites e as definições de hierarquia. Isso pode simplificar muitas das etapas de configuração posteriores.  

-   Depois de você estender o esquema, o catálogo global do Active Directory é replicado em toda a floresta. Sendo assim, planeje estender o esquema em um momento em que o tráfego de replicação não prejudique outros processos que dependem da rede:  

    -   Em florestas do Windows 2000, a extensão do esquema causa uma sincronização completa do catálogo global inteiro.  

    -   Começando com florestas do Windows 2003, apenas os atributos recém-adicionados são replicados.  

**Dispositivos e clientes que não usam o esquema do Active Directory:**  

-   Dispositivos móveis gerenciados pelo conector do Exchange Server  

-   O cliente para computadores Mac  

-   O cliente para servidores Linux e UNIX  

-   Dispositivos móveis registrados pelo Configuration Manager  

-   Dispositivos móveis registrados pelo Microsoft Intune  

-   Clientes herdados de dispositivos móveis  

-   Clientes Windows configurados para o gerenciamento de clientes somente para Internet  

-   Clientes do Windows detectados pelo Configuration Manager por estarem na Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Funcionalidades que se beneficiam da extensão do esquema  
**Instalação de computador cliente e atribuição de site**: quando um novo cliente é instalado em um computador com Windows, o cliente procura as propriedades de instalação no Active Directory Domain Services.  

-   **Soluções alternativas:** se você não estender o esquema, use uma das seguintes opções para fornecer detalhes de configuração que os computadores devem instalar:  

    -   **Usar instalação do cliente por push**. Antes de usar o método de instalação de cliente, verifique se todos os pré-requisitos foram atendidos. Para saber mais, veja a seção "Dependências do Método de Instalação" em [Pré-requisitos para a implantação de clientes em computadores com Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers).  

    -   **Instale os clientes manualmente** e forneça as propriedades de instalação de cliente usando as propriedades de linha de comando de instalação do CCMSetup. Isso deve incluir:  

        -   Especifique um ponto de gerenciamento ou um caminho de origem do qual o computador pode baixar os arquivos de instalação usando a propriedade do CCMSetup **/mp:=&lt;nome do ponto de gerenciamento nome do computador\>** ou **/source:&lt;caminho para arquivos de origem do cliente\>** na linha de comando do CCMSetup durante a instalação do cliente.  

        -   Especifique uma lista de pontos de gerenciamento iniciais para o cliente usar para que possa atribuir ao site e, então, baixar a política do cliente e as configurações do site. Use a propriedade SMSMP Client.msi do CCMSetup para fazer isso.  

    -   **Publique o ponto de gerenciamento no DNS ou no WINS** e configure os clientes para usar esse método de local do serviço.  

**Configuração de porta para comunicação de cliente para servidor** ‑ Quando é instalado, o cliente é configurado com as informações de porta armazenadas no Active Directory. Se depois você alterar a porta de comunicação de cliente para servidor de um site, um cliente poderá obter essa nova configuração de porta por meio dos Serviços de Domínio Active Directory.  

-   **Soluções alternativas:** se você não estender o esquema, use uma das opções a seguir para fornecer novas configurações de porta a clientes existentes:  

    -   **Reinstale os clientes** usando opções que configuram a nova porta.  

    -   **Implantar um script personalizado para clientes que atualiza as informações de porta**. Se os clientes não se comunicarem com um site devido à alteração da porta, você não poderá usar o Configuration Manager para implantar esse script. Por exemplo, você pode usar a Política de Grupo.  

**Cenários de implantação de conteúdo** ‑ Quando você cria o conteúdo em um site e implanta esse conteúdo em outro site na hierarquia, o site receptor deve ser capaz de verificar a assinatura dos dados do conteúdo assinado. Isso requer acesso à chave pública do site de origem em que você cria esses dados. Ao estender o esquema do Active Directory para o Configuration Manager, a chave pública do site torna-se disponível para todos os sites na hierarquia.  

-   **Solução alternativa:** se não estender o esquema, você poderá usar a ferramenta de manutenção de hierarquia, **preinst.exe**, para trocar informações de chave segura entre os sites.  

     Por exemplo, se pretende criar conteúdo em um site primário e implantar esse conteúdo em um site secundário abaixo de um site primário diferente, você deve estender o esquema do Active Directory para habilitar o site secundário a obter a chave pública de sites primários de origem, ou deve usar preinst.exe para compartilhar as chaves diretamente entre os dois sites.  

## <a name="active-directory-attributes-and-classes"></a>Classes e atributos do Active Directory  
Ao estender o esquema para o System Center Configuration Manager, as seguintes classes e atributos são adicionados ao esquema e disponibilizados para todos os sites do Configuration Manager na floresta do Active Directory.  

-   Atributos:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        em  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classes:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  

>  As extensões de esquema podem incluir atributos e classes herdadas de versões anteriores do produto, mas que não são usados pelo System Center Configuration Manager. Por exemplo:  

>   
>  -   Atributo: cn=MS-SMS-Site-Boundaries  
> -   Classe: cn=MS-SMS-Server-Locator-Point  

Você pode verificar se a lista anterior é atual exibindo o arquivo **ConfigMgr_ad_schema.LDF** da pasta **\SMSSETUP\BIN\x64** da mídia de instalação do System Center Configuration Manager.  
